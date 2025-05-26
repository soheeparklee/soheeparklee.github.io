---
title: H2, JDBC, JPA, ORM
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ H2

- 개발, 테스트 용으로 가벼운 DB

## ✅ pure JDBC

- JDBC: service가 DB를 access할 수 있도록 해줌
- 👎🏻 반복되는 코드, resource 반환 코드 등 코드 복잡

- Spring DI 덕에 기존 controller, service코드는 만지지 않고 `@Configuration`클래스만 변경해 JDBC를 사용하도록 바꿀 수 있다
- ➡️ 조각을 바꿔끼듯 ➡️ module, abstract

## ☑️ JDBC implement후 test code

- Test code: use `@Transactional` 하면 하나의 test이후에 DB초기화하도록 동작
- 테스트 후 데이터 변경 사항을 자동으로 **롤백**하기 위해
- (이전 `@AfterEach` 에서 `db clear`하던 것처럼)

```java
@SpringBootTest
@Transactional //transactional to initiate DB
class MemberServiceIntegrationTest {

    @Autowired MemberService memberService;
    @Autowired MemberRepository repository;
}
```

## ✅ Spring JDBC template

- 👍🏻 반복코드가 많은 pure JDBC보다 코드를 훨씬 간결하게 해 줌
- 👎🏻 하지만 sql query은 개발자가 직접 적어줘야 한다는 단점이 있음

```java
public class JdbcTemplateMemberRepository implements MemberRepository{
    private final JdbcTemplate jdbcTemplate; //implement JdbcTemplate
    public JdbcTemplateMemberRepository(DataSource dataSource) { //JdbcTemplate contructor
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    @Override
    public Optional<Member> findById(Long id) {
        List<Member> result = jdbcTemplate.query("select * from member where id = ?", memberRowMapper(), id); //need to write SQL
        return result.stream().findAny();
    }
}
```

## ✅ JPA

- 👍🏻 객체와 데이터베이스 테이블을 **매핑**하고 SQL 자동화
- 👍🏻 JPA가 중간에서 sql query를 대신 날려줌, sql작성하지 않아도 됨
- 👍🏻 sql, 데이터 중심 설계 ➡️ 객체 중심 설계로 전환 가능
- `Hibernate`라는 오픈소스를 사용한다

- JPA is **ORM mapping**: Object Related Mapping
- needs entity for mapping
- `@Entity`를 붙이면 이제 `Member`클래스는 JPA가 관리하는 엔티티가 된다.
- JPA는 `@Entity 클래스`를 보고 서비스와 DB를 연결, 자동으로 sql을 만들어 실행한다

```java
@Entity
public class Member {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private long id;
}
```

## ✅ JPQL

- JPA사용할 때 `entity`를 탐색하기 위해 쓰이는 query
- `Primary key`로 한번에 멤버 찾는 메소드는 JPQL없이도 가능
- 그러나 이름으로 찾기, 모두 다 찾기 등 `Primary key`외에 여러개 찾는 메소드는 JPQL 필요

- 멤버 저장하기(회원가입) ➡️ JPQL 없이 가능
- id(`Primary key`)로 멤버 한명 찾기 ➡️ JPQL 없이 가능
- 멤버 여러명 이름으로 찾기 ➡️ JPQL 필요
- 모든 멤버 다 찾아오기 ➡️ JPQL 필요

```java
@Transactional //@Transactional 필요
public class JpaMemberRepository implements MemberRepository {
    private final EntityManager em; //Entity Manager 필요

    @Override
    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class).getResultList(); //JPQL 필요
    }
}
```

## ✅ Spring JPA

- JPA와 Spring을 합쳐 access DB를 더욱 간편하게 만들어버림
- 아래 코드와 같이 `extends JpaRepository<Member, Long>`

- 기본적인 CRUD는 모두 제공됨
- 👍🏻 멤버 저장, 아이디로 찾기, 모든 멤버 다 찾기 메소드 작성할 필요가 없음
- `paging` 기술도 제공

- `findByName()`은 기본 메소드가 아니기 때문에 작성
- 👍🏻 메소드 이름에 규칙을 지켜 작성하면 `findByXXX()`, sql, JPQL작성할 필요 없음
- `findByName()`, `findByNameAndId`

```java
public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {
    //멤버 저장, 아이디로 찾기, 모든 멤버 찾기 다 가능

    //이름으로 찾기는 기본 메소드가 아님
    Optional<Member> findByName(String name);
}
```

## ✅

## ✅

## ✅

## ✅
