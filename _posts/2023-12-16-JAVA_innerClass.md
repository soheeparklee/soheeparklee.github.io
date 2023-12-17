---
title: Inner Class, Anonymous Class
categories: [JAVA, JAVA_Basics]
tags: [innerclass] # TAG names should always be lowercase
---

## ✅ 클래스 안에 또 클래스 선언하기

- 멤버 인스턴스 클래스
- static 내부 클래스
- 메소드 안에 정의된 클래스
- 익명 클래스

❓ 왜 굳이 클래스 안에 클래스를 또 만드나요?
➕ 보다 강력한 캡슐화 가능 - 외부/내부 클래스 간의 관계가 긴밀할 떄 사용하면 좋음
➕ 적절히 사용하면 유지보수 용이, 가독성 ⬆️
➖ 과하게 사용하면 클래스 비대화

## ✅ 멤버 인스턴스 클래스

외부 클래스의 필드와 클래스 접근 가능
또 외부 클래스 내에 선언된 static 내부 클래스의 필드와 클래스 접근 가능

## ✅ static 내부 클래스

외부 클래스의 static 필드만 접근 가능
static이 아닌 멤버 인스턴스 클래스에는 접근 불가
그러나 외부 클래스 내에 선언된 instance 내부 클래스의 필드와 클래스 접근 불가

## ✅ 메소드 안에 정의된 클래스

스코프는 메소드 내로 제한
외부의 필드와 클래스에 접근 가능

```java
public class Outer {
    private String outerField = "인스턴스";
    private static String outerStaticField = "클래스";

    //  💡 1. 멤버 인스턴스 클래스
    class InnerInstMember {
        //  ⭐️ 외부 클래스의 필드와 클래스 접근 가능
        private String InnerInstMemberName = outerField + " 필드로서의 클래스";
        //외부 클래스 내부에 선언된 static 클래스도 접근 가능
        private InnerStaticMember InnerStaticMember = new InnerStaticMember();
        public void InnerInstMemberFunc () {
            System.out.println(InnerInstMemberName);
        }
    }

    //  💡 2. 정적 static 내부 클래스
    //  ⭐️  내부 클래스에도 접근자 사용 가능. private으로 바꿔 볼 것
    public static class InnerStaticMember {
        //  ⭐️ 외부 클래스의 static 클래스 필드만 접근 가능
        private String InnerStaticMemberName = outerStaticField + " 필드로서의 클래스";
        // ⚠️그래서 static 아닌 outerField는 접근 불가!
        //private String notStaticImpossible = outerField;

        //  ⚠️ static이 아닌 멤버 인스턴스 클래스에도 접근 불가!
        //  private InnerInstMember innerInstMember = new InnerInstMember();
        public void InnerStaticMemberFunc () {
            // ⚠️ 인스턴스 메소드지만 클래스가 정적(클래스의)이므로 인스턴스 필드 접근 불가
            //  InnerInstMemberName += inst;
            System.out.println(InnerStaticMemberName);
        }
    }

    public void memberFunc () {
        //  💡 3. 메소드 안에 정의된 클래스
        //  스코프가 메소드 내로 제한됨
        class MethodMember {
            //  외부의 필드와 클래스에 접근은 가능
            String instSttc = outerField + " " + outerStaticField;
            InnerInstMember innerInstMember = new InnerInstMember();
            InnerStaticMember InnerStaticMember = new InnerStaticMember();

            public void func () {
                innerInstMember.InnerInstMemberFunc();
                InnerStaticMember.InnerStaticMemberFunc();
                System.out.println("메소드 안의 클래스");

                //  new Outer().memberFunc(); // ⚠️ 스택오버플로우 에러!!
            }
        }

        new MethodMember().func();
    }

    public void innerFuncs () {
        new InnerInstMember().InnerInstMemberFunc();
        new InnerStaticMember().InnerStaticMemberFunc();
    }

    public InnerInstMember getInnerInstMember () {
        return new InnerInstMember();
    }
}

```

## ✅ Anonymous Class 익명 클래스

- 다른 클래스나 인터페이스로부터 상속받아 만들어지고
- 상속받거나 오버라이드 한 메소드 사용
- 한 번만 사용되고 버려짐
  - 그래서 따로 클래스로 선언하지 않는 것임
  - 따로 클래스명도 부여하지 않음 ❌
  - 이후 다시 인스턴스를 생성할 필요가 없으므로
- 람다식

```java
//인스턴스 생성 후 바로 뒤에 메소드 오버라이드
YalcoGroup store3 = new YalcoGroup (1, "포항") {
//  원본 메소드에 public 추가
@Override
    public void takeOrder() {
        System.out.printf(
            "유일한 얄코과메기 %s 과메기를 주문해주세요.%n",
        super.intro()
        );
    }

    public void dryFish () {
    System.out.println("과메기 말리기");
    }
};
```
