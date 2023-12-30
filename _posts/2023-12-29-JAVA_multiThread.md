---
title: MultiThread
categories: [JAVA, JAVA_Basics]
tags: [multithread] # TAG names should always be lowercase
---

## ✅ Java의 Thread

Process: 실행되는 모든 프로그램, CPU위에서 돌아가고 있는 프로그램 <br>
Thread: Process 내 동시에 진행되는 **작업 갈래** <br>
여러 요리사가 동시에 요리를 처리하기<br>
<br>

- 병행처리<br>
- 병렬처리<br>

#### single thread

Main Thread 시작 <br>
main method <br>
순차적으로 실행 <br>

#### multi thread

마찬가지로 Main Thread에서 시작 <br>
병렬 실행 <br>
실행되는 순서는 매번 달라진다. <br>

### ☑️ Java Thread 작업 순서

#### 스레드 객체 생성 new

java에서는 Thread도 클래스 <br>

#### 실행 대기 Runnable

Runnable 함수형 interface 사용 <br>
Runnable 상속받은 클래스 구현 및 사용 <br>
lambda 또는 anonymous로 사용도 가능하다. <br>

#### 실행

#### 종료 Terminated

종료되면 GC가 치움 <br>

## ✅ MultiThread Programming

### ☑️ Java Thread 생성, start

```java
public class JavaThreading {
    public static void main(String[] args) {
        //thread생성
        Thread thread1= new Thread(new MyRunnable());
        Thread thread2= new Thread(new MyRunnable());
        System.out.println("main Thread name: " + Thread.currentThread().getName()+ " is running"); //main Thread name: main is running

        //start thread
        thread1.start();
        thread2.start();

        System.out.println("main Thread name: " + Thread.currentThread().getName()+ " is running");

    }

    //runnable
    static class MyRunnable implements Runnable{
        @Override
        public void run(){
            //get current thread name
            System.out.println("class MyRunnable Thread name: " + Thread.currentThread().getName()+ " is running");

            // class MyRunnable Thread name: Thread-0 is running
            // class MyRunnable Thread name: Thread-1 is running
        }
    }
}

```

### ☑️ Thread can be anonymous, Lambda

```java
public class JavaThreading {
    public static void main(String[] args) {
        //⭐️ thread생성
        Thread thread1= new Thread(new MyRunnable());
        //⭐️ anonymous thread
        Thread thread2= new Thread(new MyRunnable() {
            @Override
            public void run() {
                System.out.println("Thread name: "+Thread.currentThread().getName()+" is running");
        }
        });
        //⭐️ Lambda
        Thread thread3= new Thread(()-> System.out.println("Thread name: " + Thread.currentThread().getName()+ " is running"));

        //start thread
        thread1.start();
        thread2.start();
        thread3.start();

        System.out.println("Thread name: " + Thread.currentThread().getName()+ " is running");
    }
}
```

### ☑️ thread는 순서 정해진 것 없음

순서 보장되는 것 없음, 아주 무작위

```java
package chap59_MultiThread;

public class MultiThreadingExample {
    public static void main(String[] args) {
        //1에서 100까지 multiThreading으로 출략

        //thread 2개
        Thread thread1= new Thread(new PrintNumRunnable(1, 50));
        Thread thread2= new Thread(new PrintNumRunnable(51, 100));

        thread1.start();
        thread2.start();

        //thread 3개
        Thread thread3= new Thread(new PrintNumRunnable(1, 30));
        Thread thread4= new Thread(new PrintNumRunnable(31, 60));
        Thread thread5= new Thread(new PrintNumRunnable(61, 100));

        thread3.start();
        thread4.start();
        thread5.start();

    }
}
//▶️ 출력 결과
//1에서 50까지, 51에서 100까지 출력되는 것 ❌
//Thread는 순서는 무관하게 출력되기 때문에 1~100까지의 숫자가 마구잡이로 출력된다.
//순서가 아주 마구잡이로 출력
//만약 Thread가 한 개였다면 1~100까지 차례대로 출력되었을 것이다.

```

## ✅ 개별 영역과 공통 영역, 동기화 문제, Syncrhonize

<img width="343" alt="스크린샷 2023-12-29 오후 5 29 30" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/92aad43e-c838-4e09-b00e-26ea3b025f2f">

### ✔️ 개별 영역:

혼자 먹는 자장면 <br>
PC register, Stack Area, Native Method Stack <br>

### ✔️ 공통 영역:

같이 공유해서 먹는 탕수육 <br>
Method Area, Heap Area <br>

### 💥 thread의 동기화 문제

thread 순서가 정해지지 않아 발생하는 문제 <br>
공통 영역에 여러 개의 thread가 동시에 접속해서 수정하기 시작하면, **충돌/누락 문제 발생 가능** <br>

```java
//Counter.java
//1씩 커지는 메소드
public class Counter {
    private int count = 0;

    public void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

//IncrementRunnable.java
public class IncrementRunnable implements Runnable{
    private Counter counter;

    public IncrementRunnable(Counter counter) {
        this.counter = counter;
    }

    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            counter.increment();
            System.out.println("Count: " + counter.getCount());
        }
    }
}

//MultiThreadIssue.java
public class MultiThreadIssue {
    public static void main(String[] args) {
        Counter counter= new Counter();
        Thread thread1= new Thread(new IncrementRunnable(counter));
        Thread thread2= new Thread(new IncrementRunnable(counter));
        Thread thread3= new Thread(new IncrementRunnable(counter));

        thread1.start();
        thread2.start();
        thread3.start();
    }
}
// 하나의 counter에 대해서 thread 여러개 실행하니 3000까지 출력이 안 되고 누락이 발생할 수 있다.
```

### 🚪 thread의 동기화 해결 Syncrhonize

thread의 순서는 바꿀 수 없으니 <br>
thread의 **영역 정해주기** <br>
먼저 수정하고 있는 thread가 그 영역 수정 끝나면, 그 다음 thread가 또 수정하고... <br>
**Syncrhonize**는 일정 영역의 문을 만들어서, 한 번에 한 개의 thread만 들어와서 수정 가능 <br>
나머지 thread는 문 밖에서 기다려야 함, 그 영역에 접근할 수 없음 <br>

```java
// package chap59_MultiThread;

// public class Counter {
//     private int count = 0;

    public synchronized void increment() {
        count++;
    }

//     public int getCount() {
//         return count;
//     }
// }

```

## ✅ Server MultiThread

Server는 다수의 client의 요청을 동시에 처리해야 한다. <br>
Server는 client의 요청을 하나하나 처리하는게 아니라, 동시에 조금조금씩 처리하고 싶음 ➡️ multiThread <br>
<br>
기존의 server코드 개선하기 <br>
multi thread하기 전에는 모두 main thread 안에서 실행되고 있음 <br>
이제 main thread는 socket 열고 끝. <br>
다른 multi thread에서 data가져와서 list에 추가하기 <br>
<br>
또 list는 공통영역이니까 synchronize 해주기 <br>

```java
// ✅ main thread
public class ServerInfinite {
    public static void main(String[] args) {
        List<Customer> customerList= new ArrayList<>(); //고객 대기 리스트

        // try(ServerSocket serverSocket= new ServerSocket(1234);
        // ){
        //     System.out.println("server started");

        //     while(true){
        //         try{
        //             Socket clientSocket= serverSocket.accept();

                    //💡 multiThread
                    //main thread는 socket열고 끝
                    //다른 thread에서 input, output받도록 runnable로 넘겨버림!
                    Thread request= new Thread(new RequestHandlerRunnable(clientSocket, customerList));
                    request.start();

//                     } catch(IOException e){
//                    e.printStackTrace();
//             }
//             }
//         }catch(IOException e){
//             e.printStackTrace();
//         }
//     }
// }

// ✅ multi thread
//multi thread에서 추가하는 기능 구현
public class RequestHandlerRunnable implements Runnable{

    private Socket clientSocket;
    private List<Customer> customerList;

    public RequestHandlerRunnable(Socket clientSocket, List<Customer> customerList) {
        this.clientSocket = clientSocket;
        this.customerList = customerList;
    }

    @Override
    public void run(){
        System.out.println("client 접속하였습니다.");
try {
    InputStream clientInputStream = clientSocket.getInputStream();
    ObjectInputStream objectInputStream = new ObjectInputStream(clientInputStream);

    OutputStream serverOutputStream = clientSocket.getOutputStream();
    PrintWriter printwriter = new PrintWriter(serverOutputStream, true);

    //직렬화
    Customer customer = (Customer) objectInputStream.readObject();
    //💡customerList는 공통영역 ➡ synchronize 필요
    //customerList.add(customer); ❌
    ListUtil.addList(customerList, customer);

    // System.out.println("Thread name: " + Thread.currentThread().getName());
    // System.out.println(customer + " added to Waiting List");

    // printwriter.println("Customer waiting list: " + customerList);

    //socket 닫기
    clientSocket.close();
// } catch(Exception e){
//     e.printStackTrace();
// }
//     }
// }

// ✅ client.java
//수정한 내용이 없음
public class Client {
    // public static void main(String[] args) {

    //     try(Socket socket= new Socket("localhost", 1234)){

    //         OutputStream outputStream= socket.getOutputStream();
    //         ObjectOutputStream objectOutputStream = new ObjectOutputStream(outputStream);

    //         InputStream inputStream = socket.getInputStream();
    //         BufferedReader bufferedReader= new BufferedReader(new InputStreamReader(inputStream));

    //         Customer customer= new Customer("ID111", "Park");

    //         objectOutputStream.writeObject(customer);
    //         objectOutputStream.flush();

    //         String response= bufferedReader.readLine();
    //         System.out.println("Customer List from Server"+ response);

    //         System.out.println("Server finished");
    //     } catch (UnknownHostException e){
    //         e.printStackTrace();
    //     } catch(IOException e){
    //         e.printStackTrace();
    //     }
    // }
}
// ✅  synchronized 구현하기 위한 ListUtil.java
public class ListUtil {
    public synchronized static void addList(List<Customer> customerList, Customer newCustomer){
        customerList.add(newCustomer);
    }
}
//synchronized하기 위해 ListUtil추가한 이유는 customerList의 경우, 내가 만든 list가 아니기 때문
```
