---
title: Repository, Service, Test, springBean, component scan
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## 📌 Summary

- ✔️ **Optional**
- if there is possibility to be null, `Optional` and use `ifPresent`

- ✔️ **Test code**:
- given, when, then
- `Asssertions.assertThat()`
- for exceptions, use `Assertions.assertThrows()`
- `@AfterEach()` to clear data
- `@BeforeEach()` to inject repository in service ➡️ dependency injection

- ✔️ **Component scan, spring bean**
- `@Component`을 붙이면 `spring bean`으로 자동 등록됨
- `spring bean`으로 등록되면: `spring container`가 dependency inject
- `@Component`는 하나만 만들어 `spring container`가 관리 ➡️ singleton(하나만 unique하게 만든다)
- `@Autowired`를 써서 `spring bean`을 자동으로 inject dependency, 이제 서비스는 repository를 쓸 수 있고 controller는 서비스를 가져다 쓸 수 있음

## ✅ Repository

- `Member Repository` is interface
- `Memory Member Repository` implements `Member Repository`

```java
//interface MemberRepository
public interface MemberRepository {
    Member save(Member member);
    Optional<Member> findById(Long id);
    Optional<Member> findByName(String name);
    List<Member> findAll();
}

//MemoryMemberRepository
public class MemoryMemberRepository implements MemberRepository{
    private static Map<Long, Member> store = new HashMap<>();
    private static long sequence = 0L;

    @Override
    public Member save(Member member) {
    }

    @Override
    public Optional<Member> findById(Long id) {
    //optional: to handle if return value is null
    }

    @Override
    public Optional<Member> findByName(String name) {
    }

    @Override
    public List<Member> findAll() {
    }

    public void clearStore(){ //to clear repository after test
        store.clear();
    }
}
```

## ✅ Repository Test

- ⭐️ **After each**
- 테스트 실행 후 공유 데이터를 정리(clear)하는 코드
- `MemoryMemberRepositoryTest` test code안에는 3개의 테스트가 들어있음
- 이 3개의 테스트는 순서가 보장이 안 됨
- 따라서 한 개의 테스트가 끝나면 `repository`를 초기화해 주어야 함 ➡️ `afterEach()`

- ⭐️ `Assertions.assertThat()`을 사용해 결과 비교

```java
class MemoryMemberRepositoryTest {
    MemoryMemberRepository respository = new MemoryMemberRepository();

    @AfterEach
    public void afterEach(){
        respository.clearStore();
        //테스트는 순서 보장이 안 됨
        //테스트 하나 끝날 때마다 초기화
    }
    @Test
    public void save(){
        Member member = new Member();
        member.setName("spring");

        respository.save(member);
        Member result = respository.findById(member.getId()).get();
        assertThat(member).isEqualTo(result);
    }
    @Test
    public void findByName(){
        Member member1 = new Member();
        member1.setName("spring1");
        respository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        respository.save(member2);

        Member result = respository.findByName("spring1").get();
        assertThat(result).isEqualTo(member1);
    }

    @Test
    public void findAll(){
        Member member1 = new Member();
        member1.setName("spring1");
        respository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        respository.save(member2);

        List<Member> result = respository.findAll();
        assertThat(result.size()).isEqualTo(2);
    }
}
```

## ✅ Member Service

- ⭐️ **Optional**
- `Optional`: `null`이 될 가능성이 있는 것을 감싼다
  - 멤버를 `name`으로 찾을 때, 없을 수도 있으니(`null`) `Optional`로 감싼다
- `Optional`을 사용하면 `isPresent`를 쓸 수 있음
- 그러면 `null`일 때 ~게 하라고 쉽게 던질 수 있다
- 👎🏻 기존에는 멤버를 찾아와 `if (member == null)` 을 했어야 함
- 👍🏻 `Optional`을 사용하면 `isPresent`로 쉽게 `null`예외처리 가능

```java
class MemberService{
    //repository and constructor
    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }


//Use of Optional & ifPresent
private void validateDuplicateMember(Member member){
    Optional<Member> findMember = memberRepository.findByName(member.getName()); //없을 수도 있으니 optional로 감싼다
    findMember.ifPresent(m -> {
        throw new IllegalStateException("member already exsists");
    });

    //same code but better!
    memberRepository.findByName(member.getName())
            .ifPresent(m-> { //optional로 감싸면 ➡️ ifPresent로 있는지 확인하고 throw가능
                throw new IllegalStateException("member already exists");
            });
    }
}
```

## 💡 DI

> 서비스 객체가 자신이 의존하는 리포지토리 객체의 구현체를 직접 생성하지 않고, **외부(설정 등)에서 전달받아** 사용하는 설계 방식

## ✅ Member Serice Test

- use `given, when, then`

- ⭐️ **DI, Before Each**
- `memberService Test`가 생성될 때 `memberService`와 함께 `MemoryMemberRepository`도 생성되게 한다
- use `@BeforeEach`
- 그리고 `memberService`에 `MemoryMemberRepository`주입
- ➡️ Dependency Injection

```java
class MemberServiceTest {

    MemberService memberService;
    MemoryMemberRepository repository;

    @BeforeEach
    public void beforeEach(){
        repository = new MemoryMemberRepository();
        memberService  = new MemberService(repository); //⭐️ DI
    }

    @AfterEach
    public void afterEach(){
        repository.clearStore();
    }

    @Test
    void signUp() { // 정상 흐름
        //given
        Member member = new Member();
        member.setName("spring");
        //when
        Long saveId = memberService.signUp(member);
        //then
        Member findMember = memberService.findOne(saveId).get();
        assertThat(findMember.getName()).isEqualTo(member.getName());
    }

    @Test
    void signUpDuplicate() { //회원가입하는데 이름 중복되는 경우
        //given
        Member member1 = new Member();
        member1.setName("spring");

        Member member2 = new Member();
        member2.setName("spring"); //same name trying to signUp
        //when
        memberService.signUp(member1);
        //then
        IllegalStateException e = assertThrows(IllegalStateException.class, () -> memberService.signUp(member2));
        assertThat(e.getMessage()).isEqualTo("member already exists");

```

- ✔️ 회원가입하는데 이름 중복되는 경우 `signUpDuplicate()`
- `assertThrows(IllegalStateException.class, () -> memberService.signUp(member2))`
- 예외처리 터지면, `IllegalStateException.class`
- 이름이 다르면 회원가입 가능하도록
- 그리고 반환하는 예외처리 메세지 `assertThat`사용해서 비교하기

## 💡 Spring Bean and DI with annotation

- `@Bean`등록하는 방법
- 1️⃣ component scan with `@Autowired`
- 2️⃣ manual bean configuration with `@Configuration`

### 1️⃣ `Spring bean` with component scan

- `@Component`가 있으면 자동으로 `Spring bean`으로 등록된다.
- `@Controller`, `@Service`, `@Repository`은 모두 `@Component`의 일종이다
- `@Controller`, `@Service`, `@Repository` 라는 `annotation`을 붙여두면, 생성 시 `spring container`가 이를 알고 관리한다
- 👍🏻 `annotation`을 붙여놓으면 자동으로 `spring bean`에 등록된다
- `spring bean`에 등록된다는 의미: `spring container`가 하나만 만들어 관리한다

### **DI and Autowired**

- `@Controller` is dependent on `@Service` for accessing data
- `@Service` is dependent on `@Repository` for accessing data
- using `@Autowired`, can inject `spring bean` dependencies
- ➡️ dependency injection
- `@Autowired`을 씀으로써 controller는 service를 쓸 수 있게 되고, service는 repository를 쓸 수 있게 되는 것

### 👍🏻 Spring Bean으로 등록하면 장점

- `@Component`를 붙여놓으면 각 controller, service, repository는 하나만 만들어 `spring container`가 공유, 관리한다 ➡️ **singleton**
- 예를 들어 `member controller`, `order controller`에서 모두 `member service`를 호출하더라도 `member service`는 하나만 만든다
- `spring container`에서 해당 `spring bean`을 찾아 주입한다.

```java
@Controller
public class MemberController {

    private final MemberService memberService;
    @Autowired
    public MemberController(MemberService memberService) { //dependency injection by constructor
        this.memberService = memberService;
    }
}

@Service
public class MemberService {
    private final MemberRepository memberRepository;

    @Autowired
    public MemberService(MemberRepository memberRepository) { //dependency injection
        this.memberRepository = memberRepository;
    }
}
```

## 💡 Manual spring bean injection

- 2️⃣ Manually configure `spring bean`

- annotation을 쓰지 않고 별도 파일로 `spring bean`을 관리한다
- `@Configuration` 하고 config 파일 생성
- `@Bean`하고 service, repository를 모두 `spring bean`에 등록한다.

```java
@Configuration
public class SpringConfig {
    @Bean
    public MemberService memberService(){
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository(){
        return new MemoryMemberRepository();
    }
}
```

- 하지만 `@Controller`는 annotation으로 무조건 넣어야 한다

## ✅

## ✅

## ✅

## ✅

## ✅
