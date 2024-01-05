---
title: 2024.JAN.05(FRI) JAVA DAY 25
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til]
---

#### 유저아이디, 가고싶은 곳 입력해서 항공권 예약

```java
// 사용자는 자신의 userID와 가고 싶은 목적지를 입력하면,
// 해당 목적지로 가는 '왕복' 또는 '편도' 항공권 중 가장 출발이 빠른 항공권으로 예약을 진행합니다.
// (처음 예약은 ‘대기’ 상태로 초기화됩니다.)
// 만약 가는 목적지로 가는 항공권'이 없다고 하고 예약을 진행하지 않습니다.
// 만약 userId에 해당하는 Passenger ID가 없다면 RuntimeException를 뱉어야 합니다.
public class JDBCTest3 {
    //RDB, mySQL 접근 정보
    private static final String DB_URL = "jdbc:mysql://localhost:3306/chap_80";
    private static final String DB_USER = "root";
    private static final String DB_PASSWORD = "12341234";

    public static void main(String[] args) {
        //SQL 구문 정의
        //가고싶은 목직지로 가는 항공권 중 가장 빠른 것 하나 찾기
        String sqlQuery1 = "SELECT ticket_id" +
                " FROM airline_ticket " +
                " WHERE arrival_loc=?" +
                " ORDER BY departure_at"+
                "LIMIT 1"; //WHERE이 입력될 값, 이 값으로 검색할 예정
        //userID로 passengerID 가져오기
        String sqlQuery2 = "SELECT passenger_id" +
                " FROM passenger" +
                " WHERE user_id = ?"; //WHERE이 입력될 값, 이 값으로 검색할 예정
        //예약하는 SQL 구문
        String sqlInsert= "INSERT INTO reservation(passenger_id, airline_ticket_id, reservation_status, reserve_at" +
                "VALUES (?, ?, ?, ?) ";

        Scanner scanner = new Scanner(System.in);
        System.out.println("유저 아이디를 입력해주세요: ");
        Integer userId = Integer.valueOf(scanner.nextLine());
        System.out.println("가고 싶은 목적지를 입력해주세요: ");
        String destination = scanner.nextLine();

        try(Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            PreparedStatement preparedStatement1 = connection.prepareStatement(sqlQuery1);
            PreparedStatement preparedStatement2 = connection.prepareStatement(sqlQuery2);
            PreparedStatement preparedStatement3 = connection.prepareStatement(sqlInsert);
        ) {
            //받아온 destination
            preparedStatement1.setString(1, destination);
            ResultSet resultSet =  preparedStatement1.executeQuery();

            //ticketID
            Integer ticketID = null;
            while (resultSet.next()) {
                ticketID = resultSet.getInt("ticket_id");
            }
            System.out.println("가고싶은 목적지를 가는 티켓 ID를 찾았습니다~" + ticketID );

            if (ticketID == null) {
                System.out.println("목적지로 가는 항공권이 없습니다. 예약이 불가합니다.");
                return;
            }

            //userName
            preparedStatement2.setInt(1, userId); //받아온 userID
            ResultSet resultSet2 = preparedStatement2.executeQuery();

            Integer passengerIdRow= null;
            while (resultSet2.next()) {
                passengerIdRow = resultSet2.getInt("passenger_id");
            }

            Integer passesngerId= Optional.ofNullable(passengerIdRow).orElseThrow(() -> new RuntimeException("해당 ID가 없습니다."));


            //위 코드에서 얻어낸 passengerID로 예약내용 출력하기
            preparedStatement3.setInt(1, passesngerId);
            preparedStatement3.setInt(2, ticketID);
            preparedStatement3.setString(3, "대기");
            preparedStatement3.setDate(4, Date.valueOf(LocalDate.now()));

            preparedStatement3.executeUpdate();


        } catch (SQLException e) {
            e.printStackTrace();
        }



        }
}

```
