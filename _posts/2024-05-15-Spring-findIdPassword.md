---
title: Auth_Spring Security_findId, getNewPassword
categories: [JAVA, Spring]
tags: [security] # TAG names should always be lowercase
---

## ✅ findID

### ☑️ FindIdPasswordDto

아이디를 찾기 위해

- user name
- user phone number
  두 가지로 아이디 찾기

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class FindIdPasswordDto {
    private String myId;
    private String name;
    private String phoneNumber;

    public FindIdPasswordDto(String myId) {
        this.myId = myId;
    }

    public FindIdPasswordDto(String name, String phoneNumber) {
        this.name = name;
        this.phoneNumber = phoneNumber;
    }
}


```

### ☑️ SignController

```java
    @GetMapping("/findId")
    public ResponseDto findId(@RequestBody FindIdPasswordDto findIdPasswordDto){
        return authService.findId(findIdPasswordDto);
    }
```

### ☑️ AuthService

```java
    public ResponseDto findId(FindIdPasswordDto findIdPasswordDto) {
        User user= userJpa.findByNamePhoneNumber(findIdPasswordDto.getName(), findIdPasswordDto.getPhoneNumber())
                .orElseThrow(()-> new NotFoundException("Cannot find user with name and phone number"));
        return new ResponseDto(HttpStatus.OK.value(), "User ID found", user.getMyId());
    }
```

### ☑️ UserJpa

```java
    @Query(
            "SELECT u " +
                    "FROM User u " +
                    "WHERE u.name = :name AND u.phoneNumber = :phoneNumber "
    )
    Optional<User> findByNamePhoneNumber(String name, String phoneNumber);
```

### 💡 Result

<img width="812" alt="Screenshot 2024-05-15 at 17 38 34" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/3c17b5fa-6948-4d41-bd2e-4efe77f1ac9c">

## ✅ Get New Password

비밀번호는 암호화되어있기 때문에 복호화 불가 ❌ <br>
따라서 새로운 비밀번호를 주고, 비밀번호를 유저로 하여끔 고치도록 설정 <br>
새로운 비밀번호 설정을 위해 `RandomStringUtils.randomAlphanumeric` <br>

### ☑️ SignController

```java
    @PutMapping("/getPassword")
    public ResponseDto getNewPassword(@RequestBody FindIdPasswordDto findIdPasswordDto){
        return authService.getNewPassword(findIdPasswordDto);
    }
```

### ☑️ AuthService

```java
    public ResponseDto getNewPassword(FindIdPasswordDto findIdPasswordDto) {
        User user= userJpa.findByMyIdFetchJoin(findIdPasswordDto.getMyId())
                .orElseThrow(()-> new NotFoundException("Cannot find user with ID"));
        String newPwd = RandomStringUtils.randomAlphanumeric(10);
        user.setPassword(passwordEncoder.encode(newPwd));
        userJpa.save(user);
        return new ResponseDto(HttpStatus.OK.value(), "New Password.  "+ newPwd  + "  Please change your password");
    }
```

### 💡 Result

이제 유저는 새로운 비밀번호 `9huEoaFiCG`로 로그인이 가능하다.
이전 비밀번호로는 로그인 불가능 ❌

<img width="815" alt="Screenshot 2024-05-15 at 17 41 46" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/16f00570-c1e4-4b7c-a9f0-aa5ac0214ca0">

## ✅ Change user info

### ☑️ UserUpdateRequestDto

```java
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class UserUpdateRequestDto {
    @JsonProperty("name")
    private String name;
    @JsonProperty("my-id")
    private String myId;
    @JsonProperty("password")
    private String password;
    @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd")
    @JsonProperty("birthday")
    private Date birthday;
    @JsonProperty("phone-number")
    private String phoneNumber;

    public UserUpdateRequestDto(String password) {
        this.password = password;
    }
}

```

### ☑️ MyPageController

```java
    @PutMapping("/userInfo")
    public ResponseDto updateMyInfo(@AuthenticationPrincipal CustomUserDetails customUserDetails,
                                    @RequestBody UserUpdateRequestDto userUpdateRequestDto){
        return myPageService.updateMyInfo(customUserDetails, userUpdateRequestDto);
    }
```

### ☑️ MyPageService

```java
    public ResponseDto updateMyInfo(CustomUserDetails customUserDetails, UserUpdateRequestDto userUpdateRequestDto) {
        User user= userJpa.findByMyIdFetchJoin(customUserDetails.getMyId())
                .orElseThrow(()-> new NotFoundException("Cannot find user with myId: "+ customUserDetails.getMyId()));
        List<String> userMyIds= userJpa.findAll().stream().map(User::getName).collect(Collectors.toList());
        //ckeck already existing ID
        if(userMyIds.contains(userUpdateRequestDto.getMyId())) throw new BadRequestException("Cannot change myId, this Id already exists");
        user.setMyId(userUpdateRequestDto.getMyId());
        user.setPassword(passwordEncoder.encode(userUpdateRequestDto.getPassword()));
        user.setBirthday(userUpdateRequestDto.getBirthday());
        user.setPhoneNumber(userUpdateRequestDto.getPhoneNumber());
        userJpa.save(user);

        UserUpdateResponseDto userUpdateResponseDto= UserUpdateResponseDto.builder()
                .name(user.getName())
                .myId(user.getMyId())
                .birthday(user.getBirthday())
                .phoneNumber(user.getPhoneNumber())
                .build();

        return new ResponseDto(HttpStatus.OK.value(), "User info update success", userUpdateResponseDto);
    }
```

### 💡 Result

이제 유저가 원하는 비밀번호로 로그인 가능

<img width="807" alt="Screenshot 2024-05-15 at 17 44 53" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/b052def2-ae79-40d2-a27d-7103c01e0ace">
