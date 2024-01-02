---
title: Gradle
categories: [JAVA, JAVA_Basics]
tags: [gradle, build] # TAG names should always be lowercase
---

## ✅ JAVA build, build tool

### ✔️ java application 구현 및 실행 준비

☝🏻java application을 만들 때 비즈니즈 핵심 로직, 중요 클래스는 직접 구현 <br>
✌🏻 동시에 외부 클래스, 인터페이스 등 **JAVA library** 활용<br>
🤞🏻 코드가 잘 실행되는지 검증<br>
👌🏻 JAVA 외부 library 종속성 관리, library끼리 꼬이지 않도록(왜냐하면 library끼리 서로를 참조하기 때문)<br>
👍🏻 **JAR** 이라는 압축 파일로 패키징하여 실행 준비 끝!<br>

### ✔️ JAVA build

구현 + 실행할 수 있는 상태로 만들기 <br>
JAVA build 🟰 JAVA compile 과정 ➕ 기타 작업 <br>
<br>

- java compile <br>
  = java dependency management <br>
- java test <br>
- java assemply <br>

### ✔️ JAVA build tool

매번 정형화된 build 작업을 **자동화**해주는 시스템<br>

- make<br>
- ant: java에 특화된 빌드 툴<br>
- maven: pom.xml에 maven설정<br>
- gradle: build.gradle에 gradle설정이 되어 있음<br>

### 🔖 정형화된 빌드 작업 리스트

- JAVA compile<br>
- 코드 의존성 관리<br>
- 코드 테스트 및 리포트<br>
- 문서화 작업<br>
- 압축화 파일(.jar) 생성<br>
- 배포 과정 진행<br>

## ✅ JAVA Gradle 프로젝트 구조

<img width="460" alt="스크린샷 2024-01-01 오후 4 55 27" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/0d829c4c-f156-4644-a6a0-a72e702a5aa0">

<img width="870" alt="스크린샷 2024-01-01 오후 4 58 27" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/62787466-12db-4395-8669-9a42655f05c6">

- Project: 코드, 파일을 묶는 **최상위** 작업 단위 <br>
  Project안에 Module, gradle, src 다 있음 <br>
- Module: 코드, 파일을 묶는 작업 단위 <br>
  Module 단위로 build system 이 있음. <br>
- ./gradle: **gradle 명령 **파일 모음(wrapper) <br>
- ./src: 기타 파일 모으는 폴더 <br>
  여기안에 우리가 코드 작성 <br>
  /main 패키지, Main.java가 여기 들었음 <br>
  /test 패키지도 있음 <br>
- /main 패키지: java 실행 코드, 파일 패키지 <br>
  이 안에 resourse, org.exmaple, Main.java 들어 있다. <br>
- resourse: 실행, 테스트 할 때 사용되는 java외 파일 <br>
  .csv, png, json... <br>
- org.exmaple: java group 패키지 <br>
- Main.java: 실행 클래스 <br>
- /test 패키지: 테스트 코드, 파일 패키지 <br>

## ✅ JAVA Gradle Tasks

<img width="702" alt="스크린샷 2024-01-01 오후 5 37 59" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/fe5ba751-c79a-428b-aaaa-9a097f285845">

- 통합 Task: Task가 어떤 Task에 종속 <br>
  앞의 작업이 이루어져야 그 다음 작업이 이루어지고 <br>
  앞의 작업이 실패하면 뒤에 작업 이루어지지 않음 <br>
  <br>

- 단일 Task: 오로지 한 개의 Task <br>
  그림에서 clean <br>

![이름 없는 노트북-14](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/915edb7c-f359-44fd-97c5-3286947456e1)

## ✅ JAVA Gradle DSL: Domain Specific Languages

<img width="818" alt="스크린샷 2024-01-01 오후 5 55 01" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/4ad08c4c-5a75-4c12-b91e-71a7d75fffa0">

build.gradle같은 파일<br>
<br>

- Plugins: gradle 추가 기능 관리 <br>
  task 관리 <br>
- group: version: java 모듈 메타 정보 <br>
- repository: java 외부 라이브러리 저장소 <br>
  mavenCentral()이라는 곳에서 외부 라이브러리 들고 온다. <br>
- dependencies: 사용할 외부 java 라이브러리 관리 <br>
- Gradle Task 설정: gradle task custom 설정 <br>
  test{} 라는 곳에 쓴다. <br>

```java
plugins {
    id 'java'
    //⭐️ gradle Task 같은 gradle 기능 추가
    //plugin: task를 관리
    id 'maven-publish'
}

group = 'org.example'
version = '1.0-SNAPSHOT'
//⭐️ gradle 변수 선언
//아래 사용해보았음
var jUnitVersion= "5.9.1"

repositories {
    mavenCentral()
}

dependencies {
    testImplementation platform("org.junit:junit-bom:${jUnitVersion}")
    //testImplementation platform("org.junit:junit-bom:5.9.1")
    testImplementation 'org.junit.jupiter:junit-jupiter'
    //⭐️ dependencies 추가
    //external libraries라는 파일에 추가된다.
    // maven repository 라는 사이트에서 들고 온다.
    // https://mvnrepository.com/artifact/com.google.guava/guava
    implementation 'com.google.guava:guava:32.1.2-jre'


}
//⭐️ task custom 설정
//jar, classes 등 option 추가 가능
javadoc{
    //javadoc만들 때 이 파일은 만들지 마. 제외해
    //파일의 source root가져와서 붙이기
    exclude('org/example/Main.java');
}
test {
    useJUnitPlatform()

}
```

#### ❓ java 라이브러리는 어디에서 들고 오는가?

maven repository 라는 사이트에서 들고 온다.<br>
<https://mvnrepository.com/><br>

## ☑️ JAVA Gradle 사용해서 application 개선하기

1. 기존 코드 정상적으로 실행되는지 확인 <br>
2. 비효율적인 상황이 발생한다면 <br>
3. 구글링으로 해결책(라이브러리) 찾기 <br>
4. 라이브러리 종속성 추가 <br>
5. 실제 코드에 라이브러리 사용해서 반영 <br>
6. 정상 코드 빌드 동작 확인 <br>
   <br>
   personDTO 라는 객체를 Person으로 바꾸고 싶은데, <br>
   두 객체의 field가 <br>
   personDTO는 name이라고 하고 Person은 fullname이라고 하고 <br>
   personDTO는 age이라고 하고 Person은 years이라고 하는 상황이다. <br>
   이를 어떻게 name은 fullname이고 age는 years라고 알려줄 수 있을까? <br>

```java
//✅ build.gradle
//build.gradle에 dependencies 추가
// plugins {
//     id 'java'
// }

// group = 'org.example'
// version = '1.0-SNAPSHOT'

// repositories {
//     mavenCentral()
// }

dependencies {
    testImplementation platform("org.junit:junit-bom:5.9.1")
    testImplementation 'org.junit.jupiter:junit-jupiter'
    //⭐️ dependencies 추가
    //객체 간 mapping을 위해 MapStruct core, processor추가
    implementation 'org.mapstruct:mapstruct:1.5.3.Final'
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.5.3.Final'
}

// test {
//     useJUnitPlatform()
// }

//✅ PersonMapStruct interface에 매핑
@Mapper
public interface PersonMapStruct {
    //💡 동작원리: 싱글톤 디자인 패턴
    PersonMapStruct INSTANCE= Mappers.getMapper(PersonMapStruct.class);
    //💡 동작원리: 메타 프로그래밍
    @Mapping(source= "name", target= "fullName");
    @Mapping(source= "age", target= "years");
    Person personDTOtoPerson(PersonDTO personDTO);

}

//✅ main.java
Person person= PersonMapStruct.INSTANCE.personDTOtoPerson(personDTO);
```
