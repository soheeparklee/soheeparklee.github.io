---
title: Structural_Proxy
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅

- `Real Object`: 사장님, senior
- `Proxy`: 비서, junior
- 쉬운 일, 보안 필요 없는 일은 비서가 처리 `Proxy`
- 어려운 일이나 보안이 필요한 일은 사장님은 호출한다`Real Object`

## ✅ Types of proxy

- 1️⃣ **Lazy initialization**
- When creating the instance is very cost expensive
- 무거운 작업이 실행되어야 하는 순간까지 인스턴스 생성 미루기
- 👀 loading huge images
- 👀 heavy DB objects

- 2️⃣ **Protection Proxy**
- For security reasons, only can access instance when you have permissions
- control access permission
- 👀 security layer
- 👀 authorization checks

## ✅ Structure and Diagram

[![image.png](https://i.postimg.cc/N0PQN1bb/image.png)](https://postimg.cc/wtLKMRCs)

## 👀 Proxy for laxy initialization

#### 1. Subject Interface

```java
// Subject interface
interface Image {
    void display(); //very heavy work ➡️ real object
    String getFileName(); //light work ➡️ proxy
}
```

#### 2. Real Object

```java
class RealImage implements Image {
    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk(); //to create heavy Real image, need to load from Disk
    }

    private void loadFromDisk() { //Real object is heavy, need to load from Disk
        System.out.println("Loading " + fileName);
    }

    @Override
    public void display() {
       //senior can do the difficult work
    }

    @Override
    public String getFileName() {
        return fileName; //senior can also do easy work
    }
}
```

#### 3. Proxy

- 비서 `Proxy`가 처리하기 어려운 일은 사장님 `Real Object`을 호출해야 하므로 field에 가지고 있어야 한다

```java
class ProxyImage implements Image {
    private RealImage realImage; //need to have senior as field, to call him
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    //proxy cannot run this method on its own
    @Override
    public void display() {
        if (realImage == null) { //if senior does not exist
            realImage = new RealImage(fileName); //create senior ➡️ lazy initialization
        }
        realImage.display(); //need to call senior
    }

    //junior can do easy, light work
    @Override
    public String getFileName() {
        return fileName;
    }

    //junior can also do other easy, light work
    public String getFileExtension() {
        //work for junior
    }
}
```

#### 4. Client

```java
public class Main {
    public static void main(String[] args) {
        ProxyImage image = new ProxyImage("test_image.jpg");

        image.getFileName(); //junior's easy light job
        image.getFileExtension(); //junior's easy light job

        //junior cannot do this job ➡️ will call and create senior ➡️ senior will do the work
        image.display();
        //senior already exsits ➡️ do not need to create senior ➡️ senior will do the job
        image.display();
    }
}
```

## 👀 Proxy for protection

#### 1. Subject Interface

```java
// Subject interface
interface BankAccount {
    void withdraw(double amount); //job that needs protection
    void deposit(double amount); //job does not need protection
}
```

#### 2. Real Object

```java
// Real Subject class
class RealBankAccount implements BankAccount {
    private double balance;

    public RealBankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    //can do the job that needs protection
    @Override
    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println(
                amount + " withdrawn. Current balance: " + balance);
        } else {
            System.out.println("Insufficient balance.");
        }
    }

    @Override
    public void deposit(double amount) {
        balance += amount;
        System.out.println(
            amount + " deposited. Current balance: " + balance);
    }
}
```

#### 3. Proxy

- 보안이 필요한 일은 사장님 `Real Object`을 호출해야 하므로 field에 가지고 있어야 한다

```java
// Proxy class
class BankAccountProxy implements BankAccount {
    private RealBankAccount realBankAccount; //need to have senior as field
    private String userRole;

    public BankAccountProxy(String userRole, double initialBalance) {
        this.userRole = userRole;
        this.realBankAccount = new RealBankAccount(initialBalance);
    }

    // Check if the user has Admin access
    private boolean hasAccess() {
        return "Admin".equalsIgnoreCase(userRole);
    }

    // cannot do job that needs protection
    // check permission
    // and send the job to senior
    @Override
    public void withdraw(double amount) {
        if (hasAccess()) {
            realBankAccount.withdraw(amount);
        } else {
            System.out.println("Access denied. Only Admin can withdraw.");
        }
    }

    //call senior, but do not need protection
    @Override
    public void deposit(double amount) {
        realBankAccount.deposit(amount);
    }
}
```

#### 4. Client

```java
// Client code
public class Main {
    public static void main(String[] args) {
        // User with Admin access
        BankAccount adminAccount = new BankAccountProxy("Admin", 1000);
        adminAccount.deposit(500);   // Deposit allowed
        adminAccount.withdraw(300);  // Withdraw allowed

        // User without Admin access
        BankAccount userAccount = new BankAccountProxy("User", 1000);
        userAccount.deposit(500);    // Deposit allowed
        userAccount.withdraw(300);   // Withdraw denied
    }
}

```

## 🛠️

- `@Transactional`
- When we put `@Transactional`, we are adding `Spring proxy` in the middle
- to work for `transaction, call method, commit/rollback`

```java
@Service
public class OrderService {

    @Transactional //add transactoinal
    public void placeOrder() {
        // business logic
    }
}

// conclusion
Client
  |
Spring Proxy
  |
OrderService
```
