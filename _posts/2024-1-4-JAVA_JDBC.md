---
title: JDBC
categories: [Data, SQL]
tags: [] # TAG names should always be lowercase
---

## ✅ JDBC PROGRAMMING

**Java Database Connectivity**
JAVA에서 SQL 구문 자체를 넘겨서 RDB에서 원하는 동작을 실행하는 프로그래밍
JAVA String변수로 SQL문 작성

#### JDBC 프로그래밍 작업 순서

- Driver Manager을 통해 Connection 인스턴스를 얻는다.
- Connection을 통해 Statement을 얻는다.
- Statement을 통해 ResultSet를 얻는다.

Connection, Statement

- JAVA I/O Stream 내부 구현
- 소켓 프로그래밍 내부 구현

## ☑️ 정적으로 SQL에서 JAVA로, JAVA에서 SQL로

```java
public class JDBCTest {
    /**
     * 1. 1000원 이상 산 group singer를 구하는 SELECT 문을 JDBC로 실행해보자.
     * 2. Group_singer에 새로운 singer ”르세라핌”을 넣어 INSERT 문을 JDBC로 실행해보자.
     */

    //RDB, mySQL 접근 정보
    private static final String DB_URL= "jdbc:mysql://localhost:3306/chap_78";
    private static final String DB_USER= "root";
    private static final String DB_PASSWORD= "12341234";

    public static void main(String[] args) {
        //connection 만들기, connection close꼭 해줘야 함, autoclose
        //DriverManager가 connection 만들어준다
        //Statement는 SQL을 넣기 위해 필요하다.
        try(Connection connection= DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement= connection.createStatement();
                ){
            //여기 안에 SQL을 넣는다.
            //SQL에서 JAVA로 가져오기
            String stringSQL= "SELECT *" +
                                "FROM group_singer G" +
                                "    JOIN buy_history_1 B" +
                                "   ON G.mem_id = B.mem_id" +
                                "       WHERE B.price > 1000" ;
                   ResultSet resultSet= statement.executeQuery(stringSQL);
                   //resultSet의 다음줄이 없을 떄까지(false) 실행하세요
                   while(resultSet.next()){
                       String id= resultSet.getString("mem_id");
                       String name= resultSet.getString("mem_name");
                       long price= resultSet.getLong("price");

                       System.out.println("id:"+ id+ "name:"+ name+ "price:"+price);

                   }
                    //JAVA에서 SQL update
                   String sqlUpdate= "INSERT INTO group_singer(mem_id, mem_name, mem_number, addr, phone, height, debut_date)" +
                           "VALUES ('mem120', '르세라', 5, '서울', '01012345678', 171, '2013-06-13')";

                statement.executeUpdate(sqlUpdate);
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }

    }
}

```

## ☑️ 동적으로 data 받아오기

```java
//Console에 User ID를 치면, 선호하는 도시로 가는 왕복 항공권 정보들이 출력되어야한다.
//(단, 출발지 ‘서울’이고 ID와 출발지/도착지, 출국시간/귀국시간 이 기록. )
public class JDBCTest2 {
    //RDB, mySQL 접근 정보
    private static final String DB_URL = "jdbc:mysql://localhost:3306/chap_80";
    private static final String DB_USER = "root";
    private static final String DB_PASSWORD = "12341234";

    public static void main(String[] args) {
        //SQL 구문 정의
        String sqlQuery1 = "SELECT user_id, user_name, like_travel_place" +
                " FROM users " +
                " WHERE user_name = ? "; //WHERE이 입력될 값, 이 값으로 검색할 예정

        String sqlQuery2 = "SELECT ticket_type, departure_loc, arrival_loc, departure_at, return_at, total_price " +
                "FROM airline_ticket " +
                " WHERE departure_loc = '서울' AND ticket_type = '왕복' AND arrival_loc = ? " +
                " ORDER BY total_price";

        System.out.println("유저 이름을 입력해주세요: ");
        Scanner scanner = new Scanner(System.in);
        String userName = scanner.nextLine();

        try(Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            PreparedStatement preparedStatement1 = connection.prepareStatement(sqlQuery1);
            PreparedStatement preparedStatement2 = connection.prepareStatement(sqlQuery2);
        ) {

            preparedStatement1.setString(1, userName); //받아온 username
            ResultSet resultSet =  preparedStatement1.executeQuery();

            String place = null;
            while (resultSet.next()) {
                place = resultSet.getNString("like_travel_place");
            }
            //userName으로 선호하는 곳 출력되도록
            Optional<String> likeTravelPlace = Optional.ofNullable(place);
            String likePlace = likeTravelPlace.orElseThrow(() -> new RuntimeException());
            System.out.println("선호하는 곳은 '" + likePlace + "'");

            //위 코드에서 얻어낸 likePlace로 항공권 출력하기
            preparedStatement2.setString(1, likePlace);
            ResultSet resultSet2 = preparedStatement2.executeQuery();

            while (resultSet2.next()) {
                String ticketType = resultSet2.getNString("ticket_type");
                String departureLoc = resultSet2.getString("departure_loc");
                LocalDate departureAt = resultSet2.getDate("departure_at").toLocalDate();
                String arrivalLoc = resultSet2.getString("arrival_loc");
                LocalDate arrivalAt = resultSet2.getDate("return_at").toLocalDate();

                System.out.println("type: " + ticketType + ", 출발지: " + departureLoc + ", 도착지:  " + arrivalLoc
                        + ", 출국 시간: " + departureAt + ", 출국장소: " + arrivalAt);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        }
}

```
