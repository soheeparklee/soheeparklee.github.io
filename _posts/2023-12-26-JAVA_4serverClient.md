---
title: Server-client network, Socket, Serializable
categories: [JAVA, JAVA_Basics]
tags: [server, client, serializable, network, socket] # TAG names should always be lowercase
---

## ✅ Server-client

네트워크에 있는 데이터를 내 컴퓨터로 얻어오고, 또 다른 컴퓨터로 전달하기 <br>
정보 전달이 이루어지는 구조 <br>
Server: 데이터 response <br>
client: 데이터 request <br>

하나의 Server와 다수의 client구조로 이루어져 있다. <br>
따라서 Server가 먼저 준비가 되어 있어야 client가 요청 보낼 수 있음. <br>

## ✅ Network and Socket

Socket: 네트워크로 연결되는 게이트<br>
<br>

1. Socket 오픈: 게이트 오픈<br>
2. 오픈 Socket으로 client Socket 오픈<br>
   <br>

모든 Socket들이 연동되고 나면 데이터 전송을 위한 **stream**생성 가능<br>
stream에도 input stream, output stream이 있을 것<br>
<img width="835" alt="스크린샷 2023-12-28 오후 11 31 30" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/59bbcd4e-30f7-4114-bace-dc0c2f3c535c">

## ✅ Java socket programming

### Server

Socket 생성 및 대기 <br>

```java
public class Server {
    public static void main(String[] args) {
        //1️⃣ server socket 생성
        try(ServerSocket serverSocket= new ServerSocket(1234);
            //이렇게 try안에 적으면 autocloseable
            //네트워크 외부 리소스와 연결하기 위해서는 try-catch

            //2️⃣ client 접속 대기
            Socket clientSocket= serverSocket.accept();
        ){
            System.out.println("server started");
            System.out.println("client 접속 준비 완료 ");

            //3️⃣ client로부터 데이터 받기 위한 InputStream 생성
            //데이터 들어오기
            InputStream clientInputStream= clientSocket.getInputStream();
            //한국어 받기 위해 InputStreamReader, 속도 개선 위해 BufferedReader
            BufferedReader clientBufferedReader= new BufferedReader(new InputStreamReader(clientInputStream));

            //4️⃣ client로 데이터 보내기 위한 OutputStream 생성
            //데이터 나가기
            OutputStream serverOutputStream= clientSocket.getOutputStream();
            //flush를 해야 한다. stream 비우기
            PrintWriter printwriter= new PrintWriter(serverOutputStream, true);


            //inputLine
            //들어온 내용
            String inputLine;

            //5️⃣ client로부터 데이터를 읽고 화면에 출력
            //들어온 내용 읽다가 null되면 끝
            while((inputLine= clientBufferedReader.readLine()) != null){
                System.out.println("request from client: "+ inputLine);
                printwriter.println("Response from server");
            }
        }catch(IOException e){
            e.printStackTrace();
        }
    }
}
//autoclose썼으니까 close할 필요 없음
```

### Client

client Socket 생성하고 데이터 받아오기 <br>

```java
public class Client {
    public static void main(String[] args) {
        //1️⃣ 서버에 연결, socket 생성
        //server, client의 port 번호가 같아야 한다.
        //내가 누구인지 알려주기 위해 localhost
        try(Socket socket= new Socket("localhost", 1234)){

            //2️⃣ 서버로 데이터 보내기 위한 Output Stream
            OutputStream outputStream= socket.getOutputStream();
            //autoflush true, stream 한번 비우기
            PrintWriter clientPrintWriter = new PrintWriter(outputStream, true);

            //3️⃣ 서버에서 데이터 받아오기 위한 Input Stream
            InputStream inputStream = socket.getInputStream();
            BufferedReader bufferedReader= new BufferedReader(new InputStreamReader(inputStream));

            //4️⃣ 서버에 메세지 전송
            clientPrintWriter.println("This is client request");
            //5️⃣ 서버로부터 받은 데이터 응답 출력
            String response= bufferedReader.readLine();
            System.out.println("Response from server"+ response);
            System.out.println("Server finished");

        } catch (UnknownHostException e){
            e.printStackTrace();
        } catch(IOException e){
            e.printStackTrace();
        }
    }
}

```

## ✅ 무한루프로 서버 열어두기

그런데 데이터 한 번 주고받고 끝난 다음, server는 계속 살아있어야 하는데! <br>
➡️ 무한 루프로 다음 소켓 대기 <br>

```java
// public class ServerInfinite {
//     public static void main(String[] args) {
//         //1️⃣ server socket 생성
        // try(ServerSocket serverSocket= new ServerSocket(1234);
        // ){
        //     System.out.println("server started");
            //⭐️무한루프 돌며 서버가 계속 열려서 client 접속 대기하는 서버
            while(true){
                //2️⃣ client 접속 대기
                try(Socket clientSocket= serverSocket.accept();){
                    System.out.println("client 접속하였습니다.");

                //     //3️⃣ client로부터 데이터 받기 위한 InputStream 생성
                //     //데이터 들어오기
                //     InputStream clientInputStream= clientSocket.getInputStream();
                //     //한국어 받기 위해 InputStreamReader, 속도 개선 위해 BufferedReader
                //     BufferedReader clientBufferedReader= new BufferedReader(new InputStreamReader(clientInputStream));

                //     //4️⃣ client로 데이터 보내기 위한 OutputStream 생성
                //     //데이터 나가기
                //     OutputStream serverOutputStream= clientSocket.getOutputStream();
                //     //flush를 해야 한다. stream 비우기
                //     PrintWriter printwriter= new PrintWriter(serverOutputStream, true);

                //     //inputLine
                //     //들어온 내용
                //     String inputLine;

                //     //5️⃣ client로부터 데이터를 읽고 화면에 출력
                //     //들어온 내용 읽다가 null되면 끝
                //     while((inputLine= clientBufferedReader.readLine()) != null){
                //         System.out.println("request from client: "+ inputLine);
                //         printwriter.println("Response from server");
                // }
                    } catch(IOException e){
                    throw new RuntimeException(e);
            }
    //         }
    //     }catch(IOException e){
    //         e.printStackTrace();
    //     }
    // }
}

```

## ✅ 입력값으로 객체 받아오기

### Server

```java
public class ServerInfinite {
//     public static void main(String[] args) {
        List<Customer> customerList= new ArrayList<>();

        // //1️⃣ server socket 생성
        // try(ServerSocket serverSocket= new ServerSocket(1234);
        // ){
        //     System.out.println("server started");
            //⭐️무한루프 돌며 서버가 계속 열려서 client 접속 대기하는 서버
            while(true){
                //2️⃣ client 접속 대기
                try(Socket clientSocket= serverSocket.accept();){
                    System.out.println("client 접속하였습니다.");

                    // //3️⃣ client로부터 데이터 받기 위한 InputStream 생성
                    // //데이터 들어오기
                    // InputStream clientInputStream= clientSocket.getInputStream();
                    // //한국어 받기 위해 InputStreamReader, 속도 개선 위해 BufferedReader
                    // BufferedReader clientBufferedReader= new BufferedReader(new InputStreamReader(clientInputStream));

                    // //4️⃣ client로 데이터 보내기 위한 OutputStream 생성
                    // //데이터 나가기
                    // OutputStream serverOutputStream= clientSocket.getOutputStream();
                    // //flush를 해야 한다. stream 비우기
                    // PrintWriter printwriter= new PrintWriter(serverOutputStream, true);


                    // //inputLine
                    // //들어온 내용
                    // String inputLine;

                    //5️⃣ client로부터 데이터를 읽고 화면에 출력
                    //들어온 내용 읽다가 null되면 끝
                    while((inputLine= clientBufferedReader.readLine()) != null){
                        System.out.println("request from client: "+ inputLine);
                        //배열 사이에 , 넣어서 구분해라
                        String[] strArr= inputLine.split(",");

                        String name= strArr[1];
                        String customerID= strArr[0];

                        Customer customer= new Customer(customerID, name);
                        customerList.add(customer);

//                         printwriter.println("Customer waiting list"+ customerList);
//                 }
//                     } catch(IOException e){
//                     throw new RuntimeException(e);

//             }

//             }
//         }catch(IOException e){
//             e.printStackTrace();
//         }

//     }
// }

// ▶️ 샐행 결과
// server started
// client 접속하였습니다.
// request from client: ID123, Kim
// client 접속하였습니다.
// request from client: ID124, Lee
// client 접속하였습니다.
// request from client: ID125, Park
```

### client

```java
public class Client {
//     public static void main(String[] args) {
//         //1️⃣ 서버에 연결, socket 생성
//         //server, client의 port 번호가 같아야 한다.
//         //내가 누구인지 알려주기 위해 localhost
//         try(Socket socket= new Socket("localhost", 1234)){
//             //2️⃣ 서버로 데이터 보내기 위한 Output Stream
//             OutputStream outputStream= socket.getOutputStream();
//             //autoflush true, stream 한번 비우기
//             PrintWriter clientPrintWriter = new PrintWriter(outputStream, true);
//             //3️⃣ 서버에서 데이터 받아오기 위한 Input Stream
//             InputStream inputStream = socket.getInputStream();
//             BufferedReader bufferedReader= new BufferedReader(new InputStreamReader(inputStream));

            //4️⃣ 서버에 메세지 전송
            clientPrintWriter.println("ID125, Park");
            //5️⃣ 서버로부터 받은 데이터 응답 출력
//             String response= bufferedReader.readLine();
//             System.out.println("Customer List from Server"+ response);
//             System.out.println("Server finished");
//         } catch (UnknownHostException e){
//             e.printStackTrace();
//         } catch(IOException e){
//             e.printStackTrace();
//         }
//     }
// }
// ▶️ 샐행 결과
// Customer List from ServerCustomer waiting list[Customer(customerId=ID123, name= Kim, customerGrade=SILVER, bonusPoint=0), Customer(customerId=ID124, name= Lee, customerGrade=SILVER, bonusPoint=0), Customer(customerId=ID125, name= Park, customerGrade=SILVER, bonusPoint=0)]
// Server finished

```

## ✅ Serializable

앞서 짠 코드는 오타치게 되었을 때, 또는 생성자가 바뀌었을 때 문제가 생김 <br>
이를 해결하기 위해 ➡️ Serializable <br>

### Serializable

🆚 stream
stream에는 byte stream, 문자열 stream이 있는데 socket을 통한 stream은 무조건 byte stream이다.<br>
따라서 JAVA객체 정보를 전달할 때 꼭 byte로 바꿔서 전달을 해야 함.<br>
<br>

그래서 Serializable을 상속하여 새로운 stream인 **object stream**으로 만든다.<br>
그래서 **Serializable**을 통해 **객체**를 **byte**로 바꾸고,<br>
**역직렬화**를 통해 **byt**e를 **객체**로 바꾼다.<br>
<br>

`ByteArrayOutputStream` <br>
`ByteArrayInputStream` <br>

```java
public class SerializeExmapleTest {
    public static void main(String[] args) {
        //Serialize
        Person person = new Person("Kim", "Male", 30, "Korea", "programmer");
        //⭐️ 객체를 byte 배열로 바꿀 준비
        byte[] serializedData=null;

        //직렬화에 특화된 objectOutputStream을 얻을 수 있다.
        try (ByteArrayOutputStream bao = new ByteArrayOutputStream();
             ObjectOutputStream objectOutputStream = new ObjectOutputStream(bao);
        ) {
            objectOutputStream.writeObject(person);
            objectOutputStream.flush();
        //💡직렬화해서 객체를 byte Array로 바꾼다. 컴퓨터가 알아볼 수 있도록
            serializedData = bao.toByteArray();
            String serializedString = new String(serializedData);
            System.out.println(serializedString);
            //🖥️ 컴퓨터가 알아보는 byte
            //�� sr chap57_socket.Person/s,���E I ageL countryt Ljava/lang/String;L genderq ~ L nameq ~ L 
            //occupationq ~ xp   t Koreat Malet Kimt 
        } catch (IOException e) {
            e.printStackTrace();
        }

        //💡역직렬화해서 byte를 다시 사람이 알아볼 수 있는 객체로 바꾸자
        try(ByteArrayInputStream bai= new ByteArrayInputStream(serializedData);
            ObjectInputStream objectInputStream= new ObjectInputStream(bai);
        ){
            //🙆🏻‍♀️ data읽어와서 객체로 바꾸기, 사람이 알아볼 수 있도록
            // 객체는 object로 되어 있으니까 downcasting
            Person person1= (Person) objectInputStream.readObject();
            System.out.println(person1);
            //Person{name='Kim', gender='Male', age=30, country='Korea', occupation='programmer'}
        } catch(IOException e){
           e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

}
```

## ✅ Serializable 심화

### ☑️ serialVersionUID 고유 번호 관리

```java
//person.java
public class Person implements Serializable {
    //나중에 직렬화, 역직렬화 할 때 버전이 다를 때 오류 방지 위함
    private static final long serialVersionUID= 1L;

}
```

### ☑️ Transient로 직렬화 대상에서 제외하기

전달할 때 숨겨서 전달 되면 null로 전달된다. <br>

```java
//person.java
public class Person implements Serializable {

     //💡 transient: 직렬화할 때 숨기고 싶어
    private  transient String name;
    private String gender;
    //💡 transient: 직렬화할 때 숨기고 싶어
    private  transient int age;

//SerializeExmapleTest.java
public class SerializeExmapleTest {
    public static void main(String[] args) {
        //Serialize
        Person person = new Person("Kim", "Male", 30, "Korea", "programmer");
// ▶️ 실행 결과
//Person{name='null', gender='Male', age=0, country='Korea', occupation='programmer'}
//string은 null, int는 0
```

## ✅ Serializable 적용

socket programming과 함께 사용 <br>
아까 client, server Infinite코드 개선 <br>
이젠 server에서 split해서 받지 않고 바로바로 객체로 받을 수 있다. <br>

```java
public class ServerInfinite {
    // public static void main(String[] args) {
    //     List<Customer> customerList= new ArrayList<>();

    //     //1️⃣ server socket 생성
    //     try(ServerSocket serverSocket= new ServerSocket(1234);
    //     ){
    //         System.out.println("server started");
    //         //⭐️무한루프 돌며 서버가 계속 열려서 client 접속 대기하는 서버
    //         while(true){
    //             //2️⃣ client 접속 대기
    //             try(Socket clientSocket= serverSocket.accept();){
    //                 System.out.println("client 접속하였습니다.");

    //                 //3️⃣ client로부터 데이터 받기 위한 InputStream 생성
    //                 //데이터 들어오기
                    InputStream clientInputStream= clientSocket.getInputStream();
                    //한국어 받기 위해 InputStreamReader, 속도 개선 위해 BufferedReader
                    ObjectInputStream objectInputStream= new ObjectInputStream(clientInputStream);

                    // //4️⃣ client로 데이터 보내기 위한 OutputStream 생성
                    // OutputStream serverOutputStream= clientSocket.getOutputStream();
                    // PrintWriter printwriter= new PrintWriter(serverOutputStream, true);

                        Customer customer= (Customer) objectInputStream.readObject();
                        customerList.add(customer);

                        System.out.println(customer+ " added to Waiting List");

//                         printwriter.println("Customer waiting list: "+ customerList);

//                     } catch(IOException e){
//                    e.printStackTrace();

//             } catch (ClassNotFoundException e) {
//                     e.printStackTrace();
//                 }

//             }
//         }catch(IOException e){
//             e.printStackTrace();
//         }
//     }
// }

public class Client {
    // public static void main(String[] args) {
    //     //1️⃣ 서버에 연결, socket 생성
    //     //server, client의 port 번호가 같아야 한다.
    //     //내가 누구인지 알려주기 위해 localhost
    //     try(Socket socket= new Socket("localhost", 1234)){

    //         //2️⃣ 서버로 데이터 보내기 위한 Output Stream
    //         OutputStream outputStream= socket.getOutputStream();
    //         //autoflush true, stream 한번 비우기
    //         ObjectOutputStream objectOutputStream = new ObjectOutputStream(outputStream);

    //         //3️⃣ 서버에서 데이터 받아오기 위한 Input Stream
    //         InputStream inputStream = socket.getInputStream();
    //         BufferedReader bufferedReader= new BufferedReader(new InputStreamReader(inputStream));

            Customer customer= new Customer("ID111", "Kim");
            //4️⃣ 서버에 메세지 전송
            objectOutputStream.writeObject(customer);
            objectOutputStream.flush();

//             //5️⃣ 서버로부터 받은 데이터 응답 출력
//             String response= bufferedReader.readLine();
//             System.out.println("Customer List from Server"+ response);

//             System.out.println("Server finished");

//         } catch (UnknownHostException e){
//             e.printStackTrace();
//         } catch(IOException e){
//             e.printStackTrace();
//         }
//     }
// }


```
