---
title: Try-catch, Exception
categories: [JAVA, JAVA_Basics]
tags: [trycatch, throw, error, exception, finally, resource, autocloseable] # TAG names should always be lowercase
---

## Error(오류) 🆚 Exception(예외)

둘 다 Throwable의 class

### 💥 Error(오류)

- 컴퓨터 자체의 문제(cpu, memory 등)
- JVM에서 기인한 문제
  ➡️ 코드의 문제가 아님
- 통제 불가능 ❌
- 클래스로 관리되고 있다.

### 💥 Exception(예외)

- 통제 가능 ⭕️
  🟰 예외처리
- 클래스로 관리되고 있다.
  ✔️ Check Exception: 꼭 처리해야 하는 예외
  ✔️ Uncheck Exception: 반드시 처리해야하는 예외는 아님

#### 예시

- NullPointException
- ArrayBoundOutException 배열 10개인데 11번째 인덱스 추출
- 현실세계에 맞지 않은 요청(사람 키 음수값 넣기, 3명의 티켓값 중 2명만 결제)
- 외부 환경 변화(외부 인프라 사고 발생, 읽고 있는 파일이 삭제된다던가...)

```java
public class ExceptionTest {
    public static void main(String[] args) throws FileNotFoundException {
        System.out.println("Main method run start");
        //💥 unCheckException
        //ArrayBoundOutException
        makeUncheckedException();
        //💥 checkedException
        //빨간줄 제거 위헤 throws FileNotFoundException
        makeCheckedException();
        System.out.println("Main method end");
    }
    //💥 unCheckException
    public static void makeUncheckedException(){
        int[] intArr= {1,2,3,4,5,6,7,8,9,10};
        int index=11;

        System.out.println(intArr[index]);
    }
    //💥 checkedException
    public static void makeCheckedException() throws FileNotFoundException {
        File file= new File("src/chap50_errorexception/checkedExcpetion.txt");
        FileInputStream fs= new FileInputStream(file);
        //바로 FileInputStream에 빨간줄
        //빨간줄 없애기 위해서는 throws FileNotFoundException
        //CheckedException을 하도록 요청받아 try-catch 하거나 throw를 해야 한다.
    }

}

```

## 💥 Error(오류)이나 Exception(예외) throw

객체이기 때문에 new필요
함수 나갈 때 return ❌ throw ⭕️

## ✅ Try-catch

try: 로직 실행
catch: 예외 발생하면 실행

### try-catch 사용

```java
public class TryCatch1 {
    public static void main(String[] args) {
        System.out.println("Main method run start");
        try {
            int i = 0; //만약 i가 50의 약수였다면 try문이 실행되었을 것이다.
            int data = 50 / i; //💥 exception 발생
            System.out.println("data"+ data);
        } catch(ArithmeticException e){ // 💊 error가 ArithmeticException이라면 catch 실헹
            System.out.println("Cannot divide by 0");
            System.out.println("data"+ 0);
            e.printStackTrace(); //어떤 error발생했는지 내용 보기
        }

        System.out.println("Main method end");
    }
}

```

## ✅ Try-catch 다중처리

catch문이 여러개

### try-catch 는 여러개 선언도 가능

```java
public class TrCatch2 {
    public static void main(String[] args) {
        System.out.println("Main method running start");
        List<String> stringList= new ArrayList<>();

        stringList.add("Hello ");
        stringList.add("World ");
        stringList.add("I ");
        stringList.add("Love ");
        stringList.add(null); //💥Exception 발생, null은 대문자로 만들수가 없잖아. 이 이후로 stringList.add("Coding");는 실행이 안 됨.
        stringList.add("Coding");

        for(int i=0; i<stringList.size()+5; i++){ //💥Exception 발생, arraysize보다 더 많이 출력하려고 함
            try{
                String str= stringList.get(i);
                System.out.println(str.toUpperCase());
            } catch(NullPointerException e){ //💊
                System.out.println("Cannot change null to uppercase.");
            } catch(IndexOutOfBoundsException e){ //💊
                System.out.println("Index cannot be over arraysize.");
                break;
            }
        }
        System.out.println("Main method end");
    }
}


```

### ☑️ 첫 번째 exception 발생 이후로는 진행하지 않는다.

```java
            //💥 나누기 Arithmatic exception
            //⭐️ 첫 번째 exception 발생 이후로는 진행하지 않는다.
            int i=0;
            int data= 50/i;

            //⭐얘는 실행 안 됨
            //💥String null
            String str= null;
            System.out.println(str.toUpperCase());
```

### ☑️ try catch 다중 OR로 선언 |

두 오류 중 하나 때문에 오류나서 catch

```java
public class TryMultiCatch {
    public static void main(String[] args) {
        try{
//
        //이렇게 하나하나 Exception정의해도 되지만
//        }catch(FileNotFoundException e){
//            System.out.println("FileNotFoundException");
//            e.printStackTrace();
//        }catch(ArithmeticException e){
//            System.out.println("ArithmeticException");
//        }catch(NullPointerException e){
//            System.out.println("NullPointerException");
//        }
        }catch(FileNotFoundException e){ //💊
            System.out.println("FileNotFoundException");
            e.printStackTrace();
            //OR 사용해서 Exception
        }catch(ArithmeticException | NullPointerException e ){ //💊
            System.out.println("ArithmeticException or NullPointerException");
        }
    }
}

```

## ☑️ 파일을 읽어올 때는 꼭 exception 예외처리를 해 주어야 한다.

throw또는 try-catch 사용

```java
public class TryCatch3 {
    public static void main(String[] args) {
        try {
            FileInputStream fs = new FileInputStream("src/chap50_errorexception/test.txt");  //💥Exception 발생

            int i;
            while((i=fs.read()) != -1){ //💥Exception 발생, file읽어오기
                System.out.write(i);
            }
        } catch(FileNotFoundException e){ //💊
            System.out.println("File not found");
            e.printStackTrace();
        } catch(IOException e){ //💊
            System.out.println("Problem while reading");
        }
    }
}

```

## ✅ Exception e

모든 Exception들은 이 Exception 아래에 있다.

```java
public class TryMultiCatch {
    public static void main(String[] args) {
        try{

        }catch(FileNotFoundException e){ //💊
            System.out.println("FileNotFoundException");
            e.printStackTrace();
        }catch(ArithmeticException | NullPointerException e ){ //💊
            System.out.println("ArithmeticException or NullPointerException");
        }catch(Exception e){
            //💉모든 exception을 catch
            //어떤 exception이 발생할지 예상이 되지 않을 때, 촘촘한 거름망
            //모든 exception은 이 exception의 class
            //❗️ 단, 앞에오면 모든 오류 잡아버려 실행 자체가 안됨
            System.out.println("Exception class catch");
        }
    }
}

```

## ✅ Try-catch finally

return이든,
catch로 잡든 못 잡든,
(catch했든, catch 못했든)
try-catch 영역 이후 **무조건** 실행

### 💡 finally 이유: 리소스를 다시 컴퓨터에게 돌려주어야 하기 때문이다.

```java
public class FinallyCloseTest {
    public static void main(String[] args) throws IOException {
        System.out.println("Main method run start");
        FileInputStream fs= null;
        try {
            //🗂️ 리소스 불러옴
            fs = new FileInputStream("src/chap51_trycatch/test.txt");

            int i;
            while((i=fs.read()) != -1){
                System.out.write(i);
            }

            int myInt=10;
            int data= 100/myInt;

            //fs.close(); //🗂️ 리소스 해제 코드
            //💥 fs를 닫아야지 리소스가 해제되는데, 만약 ArithmeticException이 발생하면 리소스를 해제할 수 없는 상황이 발생한다
        } catch(FileNotFoundException e){
            System.out.println("File not found");
            e.printStackTrace();
        } catch(IOException e){
            System.out.println("Problem while reading");
        }catch (ArithmeticException e){
            System.out.println("Cannot be divided by 0");
        }finally { //리소스는 무조건 해제하도록 finally
            fs.close(); //🗂️ 리소스 해제 코드, 어떤 경우에도 리소스는 해제하도록
        }
        System.out.println("Main method end");
    }
}

```

## ✅ Try-with-resource, AutoCloseable 인터페이스

### 💡 Try-with-resource

finally쓰지 않고 **try안에 FileInputStream** 가져오면 **close**가 자동으로 실행됨
Try-with-resource는 **AutoCloseable을 상속한** class만 사용 가능하다

위의 finally코드를 Try-with-resource를 사용해서 수정

- Try-with-resource있어서 close필요 없음

```java
public class FinallyCloseTest {
    public static void main(String[] args) throws IOException {
        System.out.println("Main method run start");
        //💡 Try-with-resource
        //close하고 싶은 리소스를 try()안에 넣는다.
        try (FileInputStream fs = new FileInputStream("src/chap51_trycatch/test.txt")){
            int i;
            while((i=fs.read()) != -1){
                System.out.write(i);
            }

            int myInt=10;
            int data= 100/myInt;

        } catch(FileNotFoundException e){
            System.out.println("File not found");
            e.printStackTrace();
        } catch(IOException e){
            System.out.println("Problem while reading");
        }catch (ArithmeticException e){
            System.out.println("Cannot be divided by 0");
        }
        System.out.println("Main method end");
    }
}

```

## ✅ 예외 처리 미루기: throw

각 함수에서 try, catch로 예외 처리하지 않고 main함수로 throw해서 미뤄버린다.
❗️단, main함수는 가장 최종으로 실행되는 함수니까 throw할 수 없다.
만약 main함수도 throw해버리면 예외 처리 안 하는 셈이 된다.

발생한 곳에서 처리하지 않고, 나를 호출한 다른 함수에게 throw해서 위임하기
**발생 이유:**여러 개의 함수에서 비슷한 exception이 발생할 때 각자 함수에서 처리하는게 아니라,
main method에서 이를 한 번에 처리하기
각 함수에서 exception 처리하면 비슷한 코드가 반복되니까.

```java
public class PushExceptionTest {
    public static void main(String[] args) {

        try {
            printFile("src/chap51_trycatch/test.txt");
            //아까 미뤄둔 예외처리 모두 여기서 실행
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch(IOException e){
            e.printStackTrace();
        }

    }
    //또 해결을 main함수에게 미루기
    //throws IOException
    static void printFile(String fileName) throws IOException {
        FileInputStream fs= getFileStream(fileName);
        int i;
        while((i=fs.read()) != -1){
            System.out.write(i);
        }

    }
    //파일 미루기 하는 함수
    //원해는 try, catch로 file불러오기 exception해야 함
    //throws FileNotFoundException로 해결을 printFile함수에게 미루기
    static FileInputStream getFileStream(String fileName) throws FileNotFoundException {
        FileInputStream fs = new FileInputStream(fileName);
        return fs;
    }
}

```

### handle exceptions all at once

매우 비슷한 exception이 발생하는 두 함수에서 각각 exception 처리하는게 아니라,
main에서 한 번에 처리 ➡️ 더 효율적인 코드

```java
////거의 똑같은 exception처리하는 비효율적 코드
public class handleExceptionsAtOnce {
    public static void main(String[] args) {

        //txt file, csv file읽어오는 함수
        //두 함수 모두 비슷하게 exception처리해 주어야 한다.
        printTextFile("src/chap51_trycatch/test.txt");
        printCSVFile("src/chap51_trycatch/test.csv");


    }
    //거의 똑같은 exception처리
    public static void printTextFile(String fileName){
    if(!fileName.contains(".txt")){
        System.out.println("No Text File");
        return;
    }
    try{
        FileInputStream fs= new FileInputStream(fileName);
        int i;
        while((i= fs.read()) != -1){
            System.out.write(i);
        }
    } catch(IOException e){
        System.out.println("IOException");

        }
    }
    //거의 똑같은 exception처리
    public static void printCSVFile(String fileName){
        if(!fileName.contains(".csv")){
            System.out.println("No CSV File");
            return;
        }
        try{
            FileInputStream fs= new FileInputStream(fileName);
            int i;
            while((i= fs.read()) != -1){
                System.out.write(i);
            }
        } catch(IOException e){
            System.out.println("IOException");

        }
    }
}

```

💡 더 효율적인 코드로 변경!

```java
//main으로 throw
//main에서 처리
public class handleExceptionsAtOnce {
    public static void main(String[] args) {

        try {
            printTextFile("src/chap51_trycatch/test.txt");
            printCSVFile("src/chap51_trycatch/test.csv");
        } catch(IOException e){
            System.out.println("IOException");
        }
    }

    //txt file, csv file읽어오는 함수
    //두 함수 모두 비슷하게 exception처리해 주어야 한다.
    public static void printTextFile(String fileName) throws IOException{
    if(!fileName.contains(".txt")){
        System.out.println("No Text File");
        return;
    }

        FileInputStream fs= new FileInputStream(fileName);
        int i;
        while((i= fs.read()) != -1){
            System.out.write(i);
        }

    }

    public static void printCSVFile(String fileName) throws IOException{
        if(!fileName.contains(".csv")){
            System.out.println("No CSV File");
            return;
        }
            FileInputStream fs= new FileInputStream(fileName);
            int i;
            while((i= fs.read()) != -1){
                System.out.write(i);
            }
    }
}

```

## ✅ 직접 던지기 Check Exception

문제 발생할 수 있는 함수에서 if문을 사용해 문제 상황을 정의해두고
main함수로 exception을 throw한다.
그러면 이 문제 발생할 수 있는 함수를 main함수에서 호출했을 때 문제가 셍기는 상황이면,
빨간줄이 빡!
그래서 run하기 전에 문제가 생겼다는 것을 알 수가 있다.

exception도 class의 한 종류이고, throwable을 상속한다.
if문과 함께 예외 잡기
조건문으로 잡아서, 상위 함수로 throw하기도 한다.

문제가 생길 exception을 미리 예상하여 **if문**으로 처리해 **exception을 throw**하도록 한다.
그러면 main method가 이 문제 생길 여지 있는 method 문제 있게 부르잖아?
그러면 **빨간줄이 딱!!!** 생긴다!
그러면 main method가 이 exception을 잡아서 try, catch로 처리한다.
그러면 run하기 전에 문제 생긴다는 것을 알 수 있는거지~ ➡️ check Exception
그러면 에러 없이 실행할 수 있지!

```java
public class ThrowUncheckException {
    public static void main(String[] args) {
        System.out.println("main method start");

        //✅ getIntElement
        int result=0;
        try {
            result = getIntElement(100);
            System.out.println("array result= " + result);
        } catch(Exception e){
            System.out.println("Exception throw of getIntElement is taken care of.");
            e.printStackTrace();
        }

        //✅ getDivide
        try {
            result= getDivide(0);
            System.out.println("divide result= " + result);
        } catch(Exception e){
            System.out.println("Exception throw of getDivide is taken care of.");
            e.printStackTrace();
        }

        System.out.println("main method end");
    }

    //✅ getIntElement
    static int getIntElement(int index) throws Exception{
        int[] intArr= {1,2,3,4,5,6,7,8,9,10};

        //여기에 직접 exception 예상해서 if문으로 처리
        //만약 배열 길이보다 더 큰 값을 달라고 하면 어떡하지?
        //미리 exception처리해두자!
        //함수 이름 옆에 throws Exception추가
        //이렇게 하면 main함수에서 getIntElement 잘못 호출하면 빨간줄 뜬다!
        if(index>= intArr.length){
            throw new Exception("this index does not exist on this array");
        }

        return intArr[index];
    }
    //✅ getDivide
    static int getDivide(int num) throws Exception{
        if(num == 0){
            throw new Exception("cannot be divided with this number");
        }
        int data= 100/num;;
        return data;
    }
}

```

## ✅ 사용자 정의 예외 던지기

예를 들어, 사람의 나이인데 음수가 들어온다면?
비즈니스의 요구에 맞는 조건들을 던지도록 예외 처리하기
내 마음대로 조건 만들어두고, 이 조건을 충족하지 않으면 Exception발생하도록 하기

### 조건

- PTmemeber class
- ID는 null이 아님
- ID는 8자 이상 20자 이하
- height는 양수
- weight 양수

```java
//1️⃣ PostiveNumException.java
public class PostitiveNumException extends RuntimeException{
    public PostitiveNumException(String message) {
        super(message);
    }
}

//2️⃣ IDFormatException.java
public class IDFormatException extends RuntimeException{
    public IDFormatException(String message) {
        super(message);
    }
}

//3️⃣ PTmember.java
//member에 대한 class
//⭐️ exception 클래스들 import
import chap51_trycatch.Exception.IDFormatException;
import chap51_trycatch.Exception.PostitiveNumException;

public class PTmember {
    private String ID;
    private String name;
    private Integer height;
    private Integer weight;
    private String gender;
//⭐️ 몸무게, 키 양수여야 된다는 조건 정의
    public PTmember(String name, Integer height, Integer weight, String gender) {
        if(height<0 || weight<0){
            throw new PostitiveNumException("Height or Weight cannot be less than 0");
        }

        this.name = name;
        this.height = height;
        this.weight = weight;
        this.gender = gender;
    }
//⭐️ ID조건 정의
    public void setID(String ID) {
        if(ID == null){
            throw new IDFormatException("ID cannot be null");
        }
        if(ID.length() <4 || ID.length()>20){
            throw new IDFormatException("ID cannot be shorter than 8 or longer than 20");
        }
        this.ID = ID;
    }

    @Override
    public String toString() {
        return "PTmember{" +
                "ID='" + ID + '\'' +
                ", name='" + name + '\'' +
                ", height=" + height +
                ", weight=" + weight +
                ", gender='" + gender + '\'' +
                '}';
    }
}

//4️⃣ Main.java
public class MemeberTest {
    public static void main(String[] args) {
        PTmember member1= new PTmember("Lee", 100, 100, "Female");
        member1.setID("ABCDE");
        System.out.println(member1);
        //PTmember{ID='ABCDEFG', name='Lee', height=100, weight=100, gender='Female'}

        PTmember member2= new PTmember("Jang", -100, -100, "Male");
        member2.setID("ABCDEF");
        System.out.println(member2);
        //Height or Weight cannot be less than 0

        PTmember member3= new PTmember("Kim", 100, 100, "Male");
        member3.setID(null);
        System.out.println(member3);
        //ID cannot be null

        PTmember member4= new PTmember("Park", 100, 100, "Male");
        member4.setID("A");
        System.out.println(member4);
        //ID cannot be shorter than 8 or longer than 20
    }


}



```
