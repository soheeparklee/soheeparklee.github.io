---
title: Try-catch, throw
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
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

## ✅ 예외 미루기 throw

## ✅ 사용자 정의 예외 처리

## ✅ 커스텀 예외
