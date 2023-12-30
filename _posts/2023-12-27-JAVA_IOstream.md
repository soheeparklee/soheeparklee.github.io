---
title: Input/Output Stream
categories: [JAVA, JAVA_Basics]
tags: [input, output, stream] # TAG names should always be lowercase
---

## ✅ 자바의 입출력과 Stream

❗️ Stream collection API와는 다른 개념 <br>

### ☑️ 방향 (= 일반통행)

#### ✔️ 입력 Stream

어떤 대상으로부터 자료를 읽어들일 때 사용하는 Stream <br>

#### ✔️ 출력 Stream

파일에 저장하기 위해 <br>

### ☑️ Stream끊어 보내고 읽는 단위

bit단위로 데이터 보내기에는 너무 작고, 이걸 적당한 단위로 끊어 보내다보니 byte 또는 char <br>
<img width="494" alt="스크린샷 2023-12-28 오전 1 46 50" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/7c7bb6d6-eb98-4ae8-94bf-5274fe36bc22">

#### ✔️ 바이트 Stream

byte (8bits) <br>

#### ✔️ 문자 Stream

char (2byte) <br>

### ☑️ 출력 방법

- console 입출력 <br>
- file 입출력 <br>
- image 출력 <br>

## ✅ console 입출력

`System`은 생성하지 않아도 바로 사용 가능<br>
`System.out`<br>
`System.in`<br>
`System.err`<br>
<br>
❗️read는 항상 IOException catch<br>

### ☑️ System

```java
//알파벳 한 개 받기
public class ConsoleTest {

    public static void main(String[] args) {
        //console System.in

        int i=0;
        System.out.println("Input here please: "); //a 넣으면
        try {
            i= System.in.read();
            }
           System.out.println("input "+ i); //97
           System.out.println("input changed into(char) "+ (char) i); //a

        } catch (IOException e) {
            e.printStackTrace();
        }


    }

//문장 넣기
public class ConsoleTest {

    public static void main(String[] args) {
        //console System.in

        int i=0;
        System.out.println("Input here please: "); //i love coding넣으면
        try {
            StringBuilder sb= new StringBuilder();
            //다음중 넘어가기 전까지 i 추가하겠다
            while( (i= System.in.read()) != '\n' ){
                sb.append((char)i);
            }
            System.out.println(sb); //i love coding
        } catch (IOException e) {
            e.printStackTrace();
        }


    }
}

```

### ☑️ `Scanner`로 입력받기

```java
import java.util.Scanner;
public class ScannerTest {
    public static void main(String[] args) {
        //System.in을 Scanner안에 넣어야 한다.
        Scanner scanner= new Scanner(System.in);

        System.out.println("input name please");
        //한 줄을 읽기
        String name= scanner.nextLine();

        System.out.println("input job please");
        String job= scanner.nextLine();

        System.out.println("input age please");
        int age= scanner.nextInt();

        System.out.printf("Name is %s, job is %s, age is %d", name, job, age);
    }
}

```

## ✅ file input, output

⭐️ resource 해제 <br>
finally, close로 resourece 해제 <br>
try-with-resource로 resourece 해제 <br>
<br>
input: FileInputStream 파일 읽기 <br>
output: FileOutputStream 파일 만들기, 바이트로 파일 만들기 <br>

### ✔️ FileInputStream

```java
public class FileInputStreamTest {
    public static void main(String[] args) {
        try(FileInputStream fis= new FileInputStream("src/chap56_ioStream/Test.txt")){
            int i;
            //-1이 되기 전까지 읽기
            while((i= fis.read()) !=-1){
                System.out.print((char) i);
            }
        }catch(FileNotFoundException e){
            e.printStackTrace();
        } catch(IOException e){
            e.printStackTrace();
        }
    }
}

```

### ✔️ FileOutputStream

```java
public class FileOutputTest {
    public static void main(String[] args) {

        String content= "This is content of File";
        //append
        try(FileOutputStream fos= new FileOutputStream("src/chap56_ioStream/OutputTest.txt", true)){
            //byte 배열로 만든다. string을 byte로 변환
            //append하는 것을 true
            byte[] byteArr= content.getBytes();
            fos.write(byteArr);
            //⭐️ 기존 파일 이어쓰기 가능, 파일 이름은 그대로 두고 내용만 바꿔도 됨.

            System.out.println("txt File complete");
        }catch(FileNotFoundException e){
            e.printStackTrace();
        } catch(IOException e){
            e.printStackTrace();
        }

    }
}
```

### ✔️ 한국어 쓰기 위해 FileReader

한글은 unicode로 정의되어 있어 FileInputStream, FileOutputStream으로는 불가 <br>

```java
public class FileReaderTest {
    public static void main(String[] args) {
        try(FileReader fr= new FileReader("src/chap56_ioStream/Test.txt")){
            int i;
            while((i= fr.read()) != -1 ){
                System.out.print((char) i);
            }
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }
    }
}

```

### ✔️ 한국어 쓰기 위해 FileWriter

```java
public class FileWriterTest {
    public static void main(String[] args) {
        String content= "아기 자바 뚜루뚜뚜루";
        try(FileWriter fw= new FileWriter("src/chap56_ioStream/FileWriterTest.txt")){
//⭐️ byte로 바꾸는 과정 필요 없이 바로 write가능
            fw.write(content);
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }
    }
}
```

## ✅ read image

image는 2D Array로 되어 있다. <br>
byte stream으로 바꿔 이미지를 회전시킬 수 있다. <br>

```java
public class ImageIoTest {

    public static void main(String[] args){

        // 이미지 파일 경로
        String filePath = "src/exercise/chapter_56/Picture.png";

        try {
            File file = new File(filePath);
            BufferedImage image = ImageIO.read(file);

            // 이미지 회전하는 함수
            BufferedImage rotatedImage = rotateImage(image, 90);

            // 변환된 이미지 저장
            String outputFilePath = "src/exercise/chapter_56/Picture2.png";
            ImageIO.write(rotatedImage, "png", new File(outputFilePath));

            System.out.println("이미지 파일이 만들어졌습니다.");
        } catch (IOException e) {
            throw new RuntimeException(e);
        }


    }
}
```

## ✅ 보조 stream

🆚 기반 streamz <br>
기반 stream은 직접 파일을 읽고 쓰고, <br>
보조 stream은 기반 stream을 도와줌 <br>
<br>

- 기존 기반 stream 문자열을 지원 <br>
  byte만 지원하는 기반 stream 개선 <br>
  System.in으로 한국어 넣으면 깨지니까 보조 stream I/O stream 이 도와줌 <br>
  <br>
- 기존 기반 stream 성능, 속도 개선 <br>
  Buffered I/O는 파일 복사하는데 속도 개선 <br>
  <br>
- 기존 메소드를 쉽게 사용할 수 있도록 개선 <br>
  PrintWriter 쓰면 filewriter는 못 썼던 println 쓸 수 있음 <br>

### 💡 I/O stream

```java
//기존 방법으로는 한글 읽지 못한다. ❌
public class InputStreamReaderTest {
    public static void main(String[] args) {
        int i;
        System.out.println("Input English here please: "); //a 넣으면
        StringBuilder sb= new StringBuilder();
        try {
            while((i = System.in.read()) != '\n') {
                sb.append((char)i);

            }
            System.out.println(sb.toString());
        } catch (IOException e) {
            e.printStackTrace();
        }

//💡 I/O stream으로 개선
        int j;
        System.out.println("Input Korean here please: "); //a 넣으면
        StringBuilder sb2= new StringBuilder();
        try (InputStreamReader isr= new InputStreamReader(System.in)){
            while((j = isr.read()) != '\n') {
                sb2.append((char) j);

            }
            System.out.println(sb2.toString());
        } catch (IOException e) {
            e.printStackTrace();
        }


    }
}
```

### 💡 Buffered I/O

Buffered는 중복된 데이터를 효과적으로 다룸<br>
성능이 올라가 속도 개선<br>

```java
public class BufferedStreamTest {
    public static void main(String[] args) {
        //기존 방법은 느림
        try(FileReader fr= new FileReader("src/chap56_ioStream/ReadTest.txt");
            FileWriter fw= new FileWriter("src/chap56_ioStream/WriteTest.txt")
        ){

            int i;
            while((i= fr.read()) != -1 ){
                fw.write((char) i);
            }
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }
//💡 Buffer 사용해 속도 개선
        try(BufferedReader bfr= new BufferedReader(new FileReader("src/chap56_ioStream/BufferedReadTest.txt"));
            BufferedWriter bfw= new BufferedWriter(new FileWriter("src/chap56_ioStream/BufferedWriteTest.txt"))
        ){

            int i;
            while((i= bfr.read()) != -1 ){
                bfw.write((char) i);
            }
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }
    }
}

```

### 💡 PrintWriter

FileWriter로는 println, printf를 쓸 수가 없음! <br>
그래서 PrintWriter를 사용한다 <br>

```java
public class PrintWriterTest {
    public static void main(String[] args) {
        String filename = "src/chap56_ioStream/Test.txt"; // 출력할 파일의 이름

        try (FileWriter fileWriter = new FileWriter(filename)) {
            fileWriter.write("FileWriter를 사용한 예시입니다.\n");

            int number = 42;
            String formattedNumber = String.format("이 메서드는 형식화된 문자열을 출력합니다. 숫자: %d\n", number);
            fileWriter.write(formattedNumber);

            double value = 3.14;
            String formattedValue = String.format("format() 메서드도 형식화된 문자열을 출력할 수 있습니다. 값: %.2f\n", value);
            fileWriter.write(formattedValue);

        } catch (IOException e) {
            System.out.println("파일을 쓰는 도중 오류가 발생했습니다: " + e.getMessage());
        }

// 💡 PrintWriter로 개선
        try  (PrintWriter printWriter = new PrintWriter(filename)) {
            printWriter.println("FileWriter를 사용한 예시입니다.");

            int number = 42;
            printWriter.printf("이 메서드는 형식화된 문자열을 출력합니다. 숫자: %d\n", number);

            double value = 3.14;
            printWriter.printf("format() 메서드도 형식화된 문자열을 출력할 수 있습니다. 값: %.2f\n", value);

        } catch (IOException e) {
            System.out.println("파일을 쓰는 도중 오류가 발생했습니다: " + e.getMessage());
        }
    }
}

```
