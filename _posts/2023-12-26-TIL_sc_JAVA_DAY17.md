---
title: 2023.DEC.26(TUE) JAVA DAY 17
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, optional, enum, lambda, datetime]
---

## ✅ Optional, Enum, Lambda, Datetime

고객/주문/주문 아이템/성별/배송 상태

```java
//Customer.java
 public class Customer {
        private String name;
        private int age;
        private Gender gender;


        public Customer(String name, int age, Gender gender) {
            this.name = name;
            this.age = age;
            this.gender= gender;

        }



        public String getName() {
            return name;
        }


        @Override
        public String toString() {
            return "Customer{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    ", gender=" + gender +
                    '}';
        }
    }

//Gender.java
//enum
public enum Gender {
    MALE("male"),
    FEMALE("female");
    //genderName이 소문자일수도 있으니까
    private String genderName;
    //constructor
    Gender(String genderName) {
        this.genderName = genderName;
    }
}

//Order.java
public class Order {
        private int id;
        private Optional<Customer> customer;
        private LocalDate orderDate;
        private OrderStatus status;
        private Optional<List<OrderItem>> orderItems;

        public Order(int id, Customer customer, LocalDate orderDate, OrderStatus status, List<OrderItem> orderItems) {
            this.id = id;
            this.customer = Optional.ofNullable(customer);
            this.orderDate= orderDate;
            this.status = status;
            this.orderItems = Optional.ofNullable(orderItems);
        }

    public OrderStatus getStatus() {
        return status;
    }


        public Optional<List<OrderItem>> getOrderItems() {
            return orderItems;
        }

        public Optional<Customer> getCustomer() {return customer;}
    }

//OrderItem.java
public class OrderItem {
        private int itemId;
        private String itemName;
        private double price;
        private int quantity;

        public OrderItem(int itemId, String itemName, double price, int quantity) {
            this.itemId = itemId;
            this.itemName = itemName;
            this.price = price;
            this.quantity = quantity;
        }

        public double getTotalPrice() {
            return price * quantity;
        }

    }

//OrderStatus.java
public enum OrderStatus {
    DELIVERED("배송 완료"),
    PAID("주문 완료"),
    SHIPPED("배송 완료"),
    NOT_PAID("결제 전"),

    ON_ORDER("주문 중");

    private final String orderStatusKorean;

    OrderStatus(String orderStatusKorean) {
        this.orderStatusKorean = orderStatusKorean;
    }

    public String getOrderStatusKorean() {
        return orderStatusKorean;
    }
}

//Main.java
public class Main {
        public static void main(String[] args) {
// 1. 고객 생성합니다.
            Customer customer1 = new Customer("John Doe", 30, Gender.MALE);
            Customer customer2 = new Customer("Jane Smith", 28, Gender.FEMALE);
            Customer customer3 = new Customer("Jane ho", 23, Gender.MALE);
            Customer customer4 = new Customer("Bob", 21, Gender.FEMALE);

// 2. 주문 아이템을 만듭니다.
            OrderItem item1 = new OrderItem(1, "Keyboard", 35.99, 2);
            OrderItem item2 = new OrderItem(2, "Mouse", 19.99, 3);
            OrderItem item3 = new OrderItem(3, "Monitor", 149.99, 1);

            // 3. 주문 ItemList 제작합니다.
            List<OrderItem> orderItems1 = new ArrayList<>();
            orderItems1.add(item1);
            orderItems1.add(item2);
            orderItems1.add(item3);

            List<OrderItem> orderItems2 = new ArrayList<>();
            orderItems2.add(item1);
            orderItems2.add(item3);

            // 4. 주문 List를 만듭니다.
            List<Order> orders= new ArrayList<>();
            orders.add(new Order(1001, customer1, LocalDate.of(2023,11,9), OrderStatus.PAID, orderItems1));
            orders.add(new Order(1002, null, LocalDate.of(2023,11,9), OrderStatus.SHIPPED, orderItems2));
            orders.add(new Order(1003, customer3, LocalDate.of(2023,11,9), OrderStatus.SHIPPED, orderItems2));
            orders.add(new Order(1004, customer2, LocalDate.of(2023,11,9), OrderStatus.ON_ORDER, null));
            orders.add(new Order(1005, customer4, LocalDate.of(2023,11,9), OrderStatus.NOT_PAID, null));
            orders.add(new Order(1006, customer1, LocalDate.of(2023,11,9), OrderStatus.ON_ORDER, orderItems2));

            // 5. 오늘 주문 수 및 정산 진행합니다.
            double totalRevenue = 0;
            int totalOrderCount = 0;
            Set<OrderStatus> validStatus= new HashSet<>();
            validStatus.add(OrderStatus.DELIVERED);
            validStatus.add(OrderStatus.PAID);
            validStatus.add(OrderStatus.SHIPPED);

            for(Order order: orders){
                try {
                    Customer customer= order.getCustomer().orElseThrow(()-> {throw new RuntimeException("고객이 누락 되었습니다.");});
                    if (validStatus.contains(order.getStatus())) throw new RuntimeException(order.getCustomer() + "님의 주문이 아직 주문 처리 중입니다.");
                    List<OrderItem>orderItems= order.getOrderItems().orElseThrow(()->{throw new RuntimeException(order.getCustomer() +"님의 주문 아이템들이 누락 되었습니다.");});

                    totalOrderCount++;

                    for (OrderItem orderItem: orderItems){
                        totalRevenue += orderItem.getTotalPrice();
                    }

                } catch (RuntimeException e){
                    System.out.println(e.getMessage() + " 문제로 해당 주문은 SKIP 합니다.");
                }
            }
            System.out.println("오늘 총 " + totalOrderCount + " 주문을 처리 하여 " + totalRevenue + " 수익을 올렸습니다.");
        }
    }



```
