---
title: Structural_Adapter
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## 👍🏻

- Reusability of existing code
- can reuse existing code without having to modify it, thanks to a new adapter
- 👉🏻 OC principle
- One class does one thing, adapter class does the adapter work
- 👉🏻 Single responsibility principle
- Improve compatibility

## ✅ Adapter class

[![image.png](https://i.postimg.cc/xC69NvQ2/image.png)](https://postimg.cc/340sPDWS)

- existing code: `Account`, this is the **adaptee**
- We want to implement `UserDetails` as new code, this is **target interface**
- we expect to use the `UserDetails` now
- So, `AccountUserDetails` implements `UserDetails` and wraps an `Account`, this is the **adapter**
- 👉🏻 Adapter class implements the new code and wraps the existing code

## 1️⃣ Create adapter class

#### ✔️ **Adaptee** Account

- this `Account` existed from before
- we used this class to login

```java
public class Account {
    private String name;
    private String password;
    private String email;
}
```

#### ✔️ **Target Interface** UserDetails

- new code appeared
- new way of logging in

```java
public interface UserDetails {
    String getUsername();
    String getPassword();
}
```

#### ✔️ **Adapter** AccountUserDetails

- create the adpater class
- 1️⃣ implement new class
- 2️⃣ wrap the old class

```java
public class AccountUserDetails implements UserDetails {
    private Account account;

    public AccountUserDetails(Account account) {
        this.account = account;
    }

    @Override
    public String getUsername() {
        return this.account.getName();
    }

    @Override
    public String getPassword() {
        return this.account.getPassword();
    }
}
```

#### ✔️ **Adaptee** AccountService

- old, existing code

```java
public class AccountService {
    public Account findAccountByUserName(String username){
        Account account = new Account();
        account.setName(username);
        account.setPassword(username);
        account.setEmail(username);
        return account;
    }

    public void createNewAccount(Account account){}
    public void updateAccount(Account account){}
}
```

#### ✔️ **Target Interface** UserDetails

- new code that we want to implement

```java
public interface UserDetailsService {
    UserDetails loadUser(String username);
}
```

#### ✔️ **Adapter** AccountUserDetails

- create the adpater class
- 1️⃣ implement new class
- 2️⃣ wrap the old class

```java
public class AccountUserDetailsService implements UserDetailsService {
    AccountService accountService;

    public AccountUserDetailsService(AccountService accountService) {
        this.accountService = accountService;
    }

    @Override
    public UserDetails loadUser(String username) {
        Account accountByUsername = accountService.findAccountByUserName(username);
        return new AccountUserDetails(accountByUsername);
    }
}
```

#### ✔️ Client code

```java
public class LoginHandler {
    UserDetailsService userDetailsService;

    public LoginHandler(UserDetailsService userDetailsService) {
        this.userDetailsService = userDetailsService;
    }

    public String login(String username, String password){
        UserDetails userDetails = userDetailsService.loadUser(username);
        if(userDetails.getPassword().equals(password)){
            return userDetails.getUsername();
        }else{
            throw new IllegalArgumentException();
        }
    }
}
```

```java
public class App {
    public static void main(String[] args) {
        AccountService accountService = new AccountService();
        UserDetailsService userDetailsService = new AccountUserDetailsService(accountService);
        LoginHandler loginHandler = new LoginHandler(userDetailsService);
        String login = loginHandler.login("sohee", "sohee");
        System.out.println(login);
    }
}
```

## 2️⃣ Make existing code implement the adapter target

## 🛠️ Where adapter is used in Java

- I put array but I got list(target, what I wanted)
- I put list, but I got Enumeration(target, what I wanted)
- I put ENUM, but I got arrayList(target, what I wanted)

```java
List<String> list = Arrays.asList("a", "b", "c");
Enumeration<String> enumeration = Collections.enumeration(list);
ArrayList<String> listEnum = Collections.list(enumeration);
```

- I put `FileInputStream()`, but I got `InputStream()`(target)
- I put `InputStream` but I got `InputStreamReader`(target)

```java
InputStream is = new FileInputStream("input.txt");
InputStreamReader isr = new InputStreamReader(is);
BufferedReader reader = new BufferedReader(isr)
```

## 🛠️ Where adapter is used in Spring

- In Spring security, `UserDetails`
- `HandlerAdapter` can manage requests, and it can have different forms
- so Spring provides an `adapter` for the different forms of `HandlerAdapter`
- and allow `HandlerAdapter` to return `model view`

## ✅

#### 1️⃣

#### 2️⃣

#### 3️⃣

#### 4️⃣

- 1️⃣
- 2️⃣
- 3️⃣
- 4️⃣
  👍🏻
  👎🏻

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓
👉🏻
```
