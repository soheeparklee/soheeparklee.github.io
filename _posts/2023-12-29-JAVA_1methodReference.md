---
title: Method Reference
categories: [JAVA, JAVA_Basics]
tags: [method] # TAG names should always be lowercase
---

## ✅ 함수형 인터페이스

### ✔️ Supplier

`get`
T타입 값을 공급

### ✔️ Consumer

`accept`
T타입 값을 소비

### ✔️ Function<T, R>

`apply`
T타입 인자를 받는 함수

### ✔️ BiFunction<T, U, R>

`apply`
T, U 타입 인자를 받는 함수

### ✔️ Predicate

`test`
boolean값 반환

## ✅ 메소드 레퍼런스

메소드를 참조하고 해당 메소드의 동작을 다른 코드에서 재사용 할 수 있는 기능

### ✔️ 스태틱 메소드 참조 `Class:staticMethod`

### ✔️ 생성자 Constructor 참조 `Class::new`

supplier과 자주 사용

### ✔️ 객체 인스턴스 메소드 참조 `instance::method`

인스턴스를 일단 만들고 나서, 인스턴스 메소드 참조

### ✔️ 임의 객체 메소드 호출 `Class::MethodName`

list, array있을 때 각 index 돌면서 사용
그러면 객체의 각각 index에 대해 인스턴스 메소드처럼 동작

```java
public class MethodReferenceTest1 {
    public static void main(String[] args) {
        //💡 Static Method Reference
        //Static이니까 instance생성하지 않고도 바로 method불러올 수 있음
        Consumer<String> staticLambda= (str) -> Printer.printSmth(str); //lambda
        Consumer<String> staticMethodRef= Printer::printSmth; //method reference

        staticLambda.accept("Lambda"); //Lambda is being printed
        staticMethodRef.accept("Method Reference"); //Method Reference is being printed

        //💡Constructor Method Reference
        // 빈 생성자
        Supplier<Customer> constructorLambda= ()-> new Customer(); //lambda
        Supplier<Customer> constructorMethodRef= Customer::new; //method reference

        System.out.println(constructorMethodRef.get()); //Customer(customerId=null, name=null, customerGrade=null, bonusPoint=0)

        //또 다른 constructor부르려면
        //method reference는 빈 생성자 부르는 방법이랑 똑같지만 JAVA가 알아서 찾아줌^^
        Function<String, Customer> constructorFunctionLambda= (str)->new Customer(str); //lambda
        Function<String, Customer> constructorFunctionMethodRef= Customer::new; //method reference

        System.out.println(constructorFunctionMethodRef.apply("Kim")); //Customer(customerId=Customer1, name=Kim, customerGrade=SILVER, bonusPoint=0)

        //💡 instance의 메소드 참조
        //먼저 인스턴스 생성하고 메소드 부를 수 있음
        Customer customer1= new Customer("Lee");
        Customer customer2= new Customer("Park");

        Supplier<String> customer1String= customer1::toString; //Lee의 정보 포함해서 toString

        System.out.println(customer1String.get()); //Customer(customerId=Customer2, name=Lee, customerGrade=SILVER, bonusPoint=0)

        //💡 임의 객체 메소드 호출
        //customerList안에 있는 객체들의 method를 부르는 것
        List<Customer> customerList= Arrays.asList(
                new Customer("Jang"),
                new Customer("Yoo"),
                new Customer("Seo"),
                new Customer("Choi")
        );
        //단, foreach로 부틀 때는 class로 부른다
       customerList.forEach(Customer::printMyInfo);

//        Customer(customerId=Customer4, name=Jang, customerGrade=SILVER, bonusPoint=0)
//        Customer(customerId=Customer5, name=Yoo, customerGrade=SILVER, bonusPoint=0)
//        Customer(customerId=Customer6, name=Seo, customerGrade=SILVER, bonusPoint=0)
//        Customer(customerId=Customer7, name=Choi, customerGrade=SILVER, bonusPoint=0)

    }

}

```

## 메소드 레퍼런스 🆚 Lambda

```java
public class LambdaCompare {
    Consumer<String> func= text -> System.out.prinln(text); //lambda
    Consumer<String> func= System.out::println; //Method Reference

    Function<String, Integer> lengthStr1= string ->string.length(); //lambda
    Function<String, Integer> lengthStr2= String::length; //Method Reference

    BiFunction<String, String, Boolean> equalCheck1= (str1, str2)-> str1.equals(str2); //lambda
    BiFunction<String, String, Boolean> equalCheck2= Object::equals; //Method Reference

    BinaryOperator<Integer> maxNum1= (num1, num2) -> Math.max(num1, num2); //lambda
    BinaryOperator<Integer> maxNum2= Math::max; //Method Reference

}
```

## ✅ Stream API와 Method Reference

💡 Static Method Reference
💡 Constructor Method Reference

```java
public class StreamExmaple1 {
    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>();
        customers.add(new Customer("C001", "K"));
        customers.add(new Customer("C002", "L"));
        customers.add(new Customer("C003", "Park"));
        customers.add(new Customer("C004", "Jang"));

        // ❔ StringUtils의 isLongName static 메소드를 이용하여 3글자보다 긴 이름의 손님들 이름을 출력
        customers.stream()
                .map(customer->customer.name)
                //💡 Static Method Reference
//                .filter(name -> StringUtils.isLongName(name)) //Lambda
                .filter(StringUtils::isLongName)
//                .forEach(name-> System.out.println(name)); //Lambda
                .forEach(System.out::println);


        List<String> customerNames = Arrays.asList(
                "Jo",
                "Han",
                "Seo",
                "Choi"
        );

        // ❔ 손님들 이름을 가지고, 새로운 Customer List를 만들어라.
        List<Customer> customerList= customerNames.stream()
//                .map((name)-> new Customer(name))  //Lambda
                //💡 Constructor Method Reference
                .map(Customer::new)
                .collect(Collectors.toList());

        System.out.println(customerList);

    }
}

```

💡 instance의 메소드 참조
💡 임의 객체 메소드 호출

```java
public class StreamExample2 {
    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>();
        customers.add(new Customer("C001", "Kim"));
        customers.add(new Customer("C002", "Lee"));
        customers.add(new Customer("C002", "Lee"));
        customers.add(new Customer("C001", "Kim"));
        customers.add(new Customer("C003", "Seo"));
        customers.add(new Customer("C001", "Kim"));

        Customer myCustomer = new Customer("C001", "Kim");
        // ❔ myCustomer와 동일한 객체는 몇 개인지 출력하라.
        long count= customers.stream()
//                    .filter((customer)-> customer.equals(myCustomer)) //Lambda
                    //💡 instance의 메소드 참조
                    .filter(myCustomer::equals)
                    .count();

        System.out.println(count); //3

        // ❔ customers의 각각의 bonusPoint를 얻어라.
        List<Integer> customerPoint= customers.stream()
//                .map((customer)-> customer.getBonusPoint()) //Lambda
                //💡 임의 객체 메소드 호출
                .map(Customer::getBonusPoint)
                .collect(Collectors.toList());

        System.out.println(customerPoint);

    }
}

```
