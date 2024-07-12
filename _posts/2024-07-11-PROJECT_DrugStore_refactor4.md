---
title: TroubleShooting_Get just one user role as string from list
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## 🔴 From user role list, I want to get just one role as String

유저롤 리스트에서 역할 하나만 스트링으로 받고 싶다 <br>

## 🟡 Identify error

Each user has a user role list. <br>
The user will have just one role, but the role is saved as a list. <br>
But I would like to check just the role of the user. <br>
This is for checking the user’s role and if the user has role ADMIN, give the permission to run certain functions. <br>
<br>
And if the user does not have the role ADMIN, not let the user do such functions. <br>
<br>
Thus, get the role name from the role list, and I should fetch the very first role. <br>

## 🔵 Tryout 1. stream.map.findFirst()

```java
String role= user.getUserRole().stream().map(ur-> ur.getRole().getRoleName()).findFirst();
```

🔴 Fail. <br>
Getting role name from user role list will result in role name list. <br>
The result has to be String <br>

## 🔵 Tryout 2. Get user role name and save to role name list

```java
// Get user role name and save to role name list
List<String> role= user.getUserRole().stream().map(ur-> ur.getRole().getRoleName()).collect(Collectors.toList());
// And then find the first among the list
role.stream().findFirst()
```

🟡 Success, But there seems to be cleaner code. <br>

## 🔵 Tryout 3. Optional[ROLE_ADMIN]

```java
Optional<String> role=
```

🔴 Fail. <br>
Need to get result as String to compare, however the result of this code will return optional. <br>
The result has to be String <br>

## 🟢 Solution

```java
role.stream().findFirst().get().equals("ROLE_ADMIN")
```

🟢 Success. <br>
First, to get rid of Optional do findFirst(), then to compare the value use get() <br>
<br>
First, unwrap the Optional returned by findFirst() and then compare its value to "ROLE_ADMIN". <br>
You can do this using the isPresent() and get() methods of the Optional class. <br>
