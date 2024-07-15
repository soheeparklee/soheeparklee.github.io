---
title: Implement swagger 3
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## ✅ swagger v3

## 🔴 HTTPS CORS error

However, there kept happening a CORS error <br>
<img width="488" alt="1" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/c9f96f0f-5e8b-4240-b099-0fc15c5f8cdb">

### 🔵 What I tried

In browser, I was using `https`. <br>
However, the `generated server url` in swagger seemed to be `http` <br>
So I decided to change `http` to `https`. <br>

<img width="797" alt="image" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/c0cfed9c-f747-4d6c-8c57-d5d05add35fc">

### 🟢 Solution

In `SwaggerConfig`, I added `server` and `server url` <br>

```java
@Configuration
@OpenAPIDefinition(
        info = @io.swagger.v3.oas.annotations.info.Info(
                title = "DrugstoreShop project",
                description = "원하는 상품을 장바구니에 담아 살 수 있는 기능을 제공합니다",
                version = "1.0.0"
        ),
        servers = {
                @Server(url = "https://drugstoreproject.shop", description = "Generated server url") //🟢 add server url
        }
)

public class SwaggerConfig {
  //swagger config
}
```

Now, the page looks like this. <br>
And the CORS error was gone. <br>
<img width="991" alt="image" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/160fbb06-7219-4569-b364-3ce186a96b18">

## 🔴 Required Token Problem

The cors error was fixed, and APIs that **do not require tokens** were run successfully. <br>
However, we stil need to fix the problem of APIs that **need token**. <br>
If APIs are run without token, I got a `500` error. <br>

<img width="1123" alt="Screenshot 2024-07-10 at 16 58 55" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/a77f6d3f-e16c-4eff-b3c2-6263d4beeafe">

### 🔵 Identify cause of error

THe problem is because there is no token, when the API requires token. <br>

### 🟢 Add token in swagger

✔️ add build.gradle <br>

```java
 implementation 'org.springdoc:springdoc-openapi-ui:1.7.0'
```

✔️ add to `SwaggerConfig` <br>
💡 Reference <https://velog.io/@ryulkim/Spring-boot-JWT%EC%99%80-Swagger-JWT-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0> <br>

```java
private SecurityScheme createAPIKeyScheme() {
    return new SecurityScheme().type(SecurityScheme.Type.HTTP)
        .bearerFormat("JWT")
        .scheme("bearer");
}
```

## 🔴 HTTP Error

However, it was not run. <br>
There seemed to be HTTP error. <br>
The blog reference uses `http`, whereas I am using `https` <br>

### 🔵 Swagger Security Scheme type

I realized there are various Swagger Security Scheme types. <br>
💡 Reference <https://swagger.io/docs/specification/authentication/basic-authentication/> <br>
💡 Reference <https://swagger.io/docs/specification/authentication/api-keys/> <br>
<br>
I leaned that I have to use `APIKEY`. <br>
If I am using HTTPS/SSL, I have to use type `APIKEY`. <br>
<br>

### 🟢 change type to APIKEY

```java
    private SecurityScheme createAPIKeyScheme() {
        return new SecurityScheme()
                .type(SecurityScheme.Type.APIKEY)
                .in(SecurityScheme.In.HEADER)
                .bearerFormat("JWT")
                .scheme("bearer");
    }
```

Finally, I made `Authorize` button in swagger. <br>
I could `login` and get the token. <br>
And also I could put token in the `Authorize` button. <br>

<img width="931" alt="1" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/d2e588c3-3ba6-4267-93ac-5a86b9e24960">
<img width="556" alt="2" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/c1700c19-5034-4be7-87ad-1bee8725053b">

## 🔴 Header name difference error

However, for some reason, it would not recognize the token. <br>

### 🔵 Identify cause of error

I looked closely at `postman`, `developer tools` and `swagger`, <br>
I realized the name of `developer tools` and `swagger` is different! <br>
<br>

- Developer tools token <br>
  name of token is `Token` <br>
  <img width="413" alt="1" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/c3018114-80ba-4262-8626-97f2a0f658fc">

- Swagger token <br>
  name of token is `Authorization` <br>
  <img width="1443" alt="2" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/ac14f267-2993-4d79-a00f-69c16e9afdb9">

### 🟢 Change the token header name of swagger

I decided to change the swagger token header name. <br>

```java
public class SwaggerConfig {
    @Bean
    public OpenAPI openAPI() {
        return new OpenAPI().addSecurityItem(new SecurityRequirement().
                        addList("Bearer token"))
                .components(new Components().addSecuritySchemes
                        ("Bearer token", createAPIKeyScheme())) //🟢 change
                .info(new Info().title("DrugstoreShop project")
                        .description("원하는 상품을 장바구니에 담아 살 수 있는 기능을 제공합니다.")
                        .version("1.0.0"));
    }

    private SecurityScheme createAPIKeyScheme() {
        return new SecurityScheme()
                .type(SecurityScheme.Type.APIKEY)
                .in(SecurityScheme.In.HEADER)
                .name("token") //🟢 change
                .bearerFormat("JWT")
                .scheme("bearer");
    }

}
```

<img width="1160" alt="Screenshot 2024-07-10 at 22 17 10" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/71e9fd20-46f4-4827-adc5-062e3fc0706d">

Finally, all APIs recognize the token and works perfectly. <br>
My swagger has been finished! <br>

## 🟢 Swagger Link

<https://drugstoreproject.shop/swagger-ui/index.html#/> <br>
