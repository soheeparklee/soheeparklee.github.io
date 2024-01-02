---
title: 2024.JAN.01(THU) JAVA DAY 21
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, singleton, map]
---

## ✅ singleton, map

```java
//Book.java
public class Book {
    private String title;
    private String author;

    public Book() {
    }

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public void displayInfo() {
        System.out.println("책 제목: " + title + "이고, 작가는 " + author + "입니다.");
    }
}

//Car.java
public class Car {
    private int year;
    private String color;

    public Car() {
    }

    public Car(int year, String color) {
        this.year = year;
        this.color = color;
    }

    public void drive() {
        System.out.println(year + "년식 자동차를 주행합니다.");
    }

    public void stopEngine() {
        System.out.println(year + "년식 자동차의 시동을 끕니다.");
    }

    public void showInfo() {
        System.out.println("이 차의 년식: " + year + "이고, 색상은 " + color + "입니다.");
    }
}

//Singleton.java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.METHOD, ElementType.TYPE})
//TYPE: class, interface
public @interface Singleton {
    String name();

}

//SingletonConfig.java
public class SingletonConfig {
    @Singleton(name = "book")
    public Book makeBook(){
        return new Book("title", "author");
    }

    @Singleton(name = "book2")
    public Book makeBook2(){
        return new Book("title2", "author2");
    }

    @Singleton(name = "car")
    public Car makeCar(){
        return new Car(2022, "red");
    }

    @Singleton(name = "car3")
    public Car makeYellowCar(){
        return new Car(2021, "yellow");
    }
}

//SingletonContext.java
public class SingletonContext {
    private static SingletonConfig config;
    private static Map<String, Method> singletonMap = new HashMap<>();
    private static Map<String, Object> singletonObjectMap = new HashMap<>();

    public static void setConfig(SingletonConfig config) {
        SingletonContext.config = config;
    }

    static synchronized Object getSingleton(String name) throws
        //name에 해당하는 싱글톤 객체를 반환한다.
        InvocationTargetException, IllegalAccessException{
        //주어진 name에 해당하는 객체가 있는지 확인한다.
            Object singletonObject = singletonObjectMap.get(name);
        //없으면 config객체를 총해 싱글톤 패턴을 구현한 클래스에서 생성된다.
            if (singletonObject == null){
                singletonObject= singletonMap.get(name).invoke(config);
                singletonObjectMap.put(name, singletonObject);
        }
        return singletonObject;
    }

    public static void executeMethodsBySingletonAnnotation(Object object) {
        //주어진 object가 가지고 있는 메소드를 검사한다.
        //@Singleton Annotation이 적용된 메소드를 찾아 그 메소드와 이름을 map에 저장한다.
        Class<?> clazz = object.getClass();
        Method[] methods= clazz.getDeclaredMethods();

        for(Method method:methods){
            Annotation[] annotations = method.getDeclaredAnnotations();
            for(Annotation annotation:annotations){
                if(annotation instanceof Singleton){
                    Singleton singletonAnnotation= (Singleton) annotation;
                    String name= singletonAnnotation.name();
                    singletonMap.put(name, method);
                }
            }
        }
    }
}

//Main.java
public class Main {
    public static void main(String[] args) throws InvocationTargetException, IllegalAccessException {
        SingletonConfig singletonConfig = new SingletonConfig();

        SingletonContext.executeMethodsBySingletonAnnotation(singletonConfig);
        SingletonContext.setConfig(singletonConfig);

        Book book = (Book) SingletonContext.getSingleton("book");
        Book bookCopy1 = (Book) SingletonContext.getSingleton("book");
        Book bookCopy2 = (Book) SingletonContext.getSingleton("book");

        Book book2 = (Book) SingletonContext.getSingleton("book2");

        Car redCar = (Car) SingletonContext.getSingleton("car");
        Car yellowCar = (Car) SingletonContext.getSingleton("car3");
        Car yellowCar2 = (Car) SingletonContext.getSingleton("car3");

        book.displayInfo();
        bookCopy1.displayInfo();
        bookCopy2.displayInfo();

        System.out.println("두 객체는 같나요? " + ( book == bookCopy1 ) );

        book2.displayInfo();

        redCar.showInfo();
        yellowCar.showInfo();
        yellowCar2.showInfo();

        System.out.println("두 객체는 같나요? " + ( redCar == yellowCar ) );
        System.out.println("두 객체는 같나요? " + ( yellowCar == yellowCar2 ) );
    }
}

//    책 제목: title이고, 작가는 author입니다.
//        책 제목: title이고, 작가는 author입니다.
//        책 제목: title이고, 작가는 author입니다.
//        두 객체는 같나요? true
//        책 제목: title2이고, 작가는 author2입니다.
//        이 차의 년식: 2022이고, 색상은 red입니다.
//        이 차의 년식: 2021이고, 색상은 yellow입니다.
//        이 차의 년식: 2021이고, 색상은 yellow입니다.
//        두 객체는 같나요? false
//        두 객체는 같나요? true



```
