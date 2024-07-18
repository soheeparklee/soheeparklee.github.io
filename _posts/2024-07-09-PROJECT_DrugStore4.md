---
title: TroubleShooting_Instance connection lost
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## 🔴 Instance connection problem

> After 5~6 hours after deployment with nohup, at some point the connection was lost.

## 🟠 Situation Analysis

- EC2 Instance in AWS was running without problem.
- connected with ubuntu by SSH connection

<img width="1199" alt="Screenshot 2024-07-09 at 23 47 39" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/48d10c48-3b7f-4963-ba1d-7333067e6139">

- running command was as following

```bash
nohup java -jar ./build/libs/drug_store_be-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod >>/dev/null 2>&1 &
```

- and when checked `ltpn`, the four digit numbers were shown.

```bash
netstat -ltpn
```

<img width="994" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/332e6613-44ae-4d6e-b913-cca78cbf83b4">

- However, after 5~6 hours, the conenction was lost.
- And when tried to run `netstat -ltpn`, nothing was printed.

## 🔵 Tryout1: nohup.out

- Intended to look at `nohup.out` file.
- Altered the command to following.

```bash
nohup java -jar ./build/libs/drug_store_be-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod &
```

- As a result, `nohup.out` file was created.
- Ran the following commands to see `nohup.out` file.

```bash
tail -f nohup.out
```

- And after 5~6 hours when the instance lost connection, ran the following command to see `nohup.out` file.

```bash
tail -n 100 nohup.out
```

### ✔️ Result

- However, in the `nohup.out` file there does **not** seem to be any error.
  <img width="1470" alt="Screenshot 2024-07-09 at 18 16 36" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/c5a74c47-c5ee-4f4f-87dd-1562ea23e9d8">

## 🔵 Tryout2: SWAP

Maybe there is too little memory? I am using t2.micro for EC2. <br>

 <img width="696" alt="image" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/d172187c-e461-4f67-a55f-a96351250131">

### 🟠 SWAP

> space on HDD or SSD for temporarily holding data <br>
> that is not actively being used on RAM <br>
> acts as overflow area for your computer's memory <br>
> SWAP은 EC2에 한정된 방법이 아니라 LinuxOS에서 가상 메모리 관리 시스템에서 사용되는 방법<br> > <br>

> LinuxOS애서 프로세스는 주로 RAM에 적재되어 실행된다. <br>
> 그런데 시스템의 물리적인 RAM 용량보다 더 많은 메모리가 필요한 상황 발생 가능<br>

#### ✔️ Paging

> When RAM is fully utilized, os can move inactive pages of memory to swap space
> Thus, freeing RAM for other tasks.
> 🔴 Like my situation, where I need more memory<br>
> SWAP will be used as an alternative memory space<br>
> SWAP uses hard disk to make more memory<br>

#### ✔️ How does SWAP help?

- extend virtual memory
  - virtual memory: RAM + SWAP space(RAM looks bigger storage that it really has)
- handle memory overcommitment: paging
- prevent OOM errors
  - OOM: Out of Memory
  - safety net when system is out of physical RAM
  - graceful degradation

#### ✔️ check current SWAP

```bash
free -h
```

<img width="494" alt="Screenshot 2024-07-09 at 18 18 44" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/17d1d918-6db9-4798-874c-bc4c09c42138">

- As can see, there is no swap

#### ✔️ Create the SWAP file

I wanted to make a SWAP file of 4GB

```bash
sudo fallocate -l 4G /swapfile
```

#### ✔️ Set the correct permissions

```bash
sudo chmod 600 /swapfile
```

#### ✔️ Set up the SWAP area

```bash
sudo mkswap /swapfile
```

#### ✔️ Enable the Swap File

```bash
sudo swapon /swapfile
```

#### ✔️ Verify the Swap

```bash
sudo swapon --show
```

#### ✔️ Make the Swap File Permanent

- To ensure the swap file is used at boot, add it to /etc/fstab

```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

- Now, run `free -h` and you will see 4GB SWAP file created.
- However, the instance connection lost problem was **NOT** solved.
  <img width="643" alt="Screenshot 2024-07-09 at 18 26 40" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/3cea6205-b967-4170-8605-64628ab76232">

## 💡 Useful bash commands

#### ✔️ Check Disk Capacity

```bash
df -h
```

<img width="344" alt="Screenshot 2024-07-10 at 00 20 18" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/5689f74a-e506-4ebf-8111-fbcb24f8e1ce">

#### ✔️ Check Memory

```bash
free -h
```

<img width="498" alt="Screenshot 2024-07-10 at 00 20 33" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/995aa742-f0ea-464b-b25d-68e5d23ff7ba">

#### ✔️ Check Instant Capacity

실시간 용량 모니터링

```bash
watch -n -1 --add command
watch -n -1 free -h
```

<img width="667" alt="Screenshot 2024-07-10 at 00 19 43" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/45b887eb-d0df-4e62-9dbd-dd1793256f6e">

#### 💡 Reference

<https://velog.io/@kwontae1313/AWS-EC2-%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%9A%A9%EB%9F%89-%EC%A6%9D%EC%84%A4>

## 🔵 Tryout 3: Invalid character found in method name

After SWAP, the error was not fixed.
Instance connection was down again🥲
But this time, nohup.out showed me something.

### 🔴 Error: Invalid character found in method name

- nohup.out
  🔴 Error: `Invalid character found in method name. HTTP method names must be tokens`
  <img width="1055" alt="Screenshot 2024-07-10 at 14 15 05" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/758cb1ba-b1d8-49c5-989a-583d223734e7">

#### 💡 Reference

<https://medium.com/@beganjimoni23/invalid-character-found-in-method-name-http-method-names-must-be-tokens-11678f35f67f>

In the blog reference, it said to update the `build.gradle` implementation `spring-cloud-starter-netflix-eureka-client` <br>

### 🟢 Compatible versions

The cause of first error was that the degraded version of Spring Boot parent and Spring cloud version was not compatible.

💡 Spring Boot Parent

- Spring Boot provides a POM.
- This parent POM includes configurations and dependency management, for simplifying project setup for SpringBoot.

💡 Spring Cloud

- Spring Cloud builds on Spring Boot
- provides tools for building distributed systems.

Thus, I decided to update my `build.gradle`<br>

#### ✔️ build.gradle

```bash
implementation 'org.springframework.boot:spring-boot-starter-actuator'
implementation 'org.springframework.cloud:spring-cloud-starter-gateway'
implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
```

Then, I had a new error!

#### 🔴 Unable to load io.netty.resolver

🔴 Error: Unable to load io.netty.resolver.dns.macos.MacOSDnsServerAddressStreamProvider

#### 💡 Reference

<https://medium.com/@boysbee/unable-to-load-io-netty-resolver-dns-macos-macosdnsserveraddressstreamprovider-46d89bf74d42>

So I decied to change the `build.gradle` file again.
And the `netty` error was gone.

```bash
implementation{
      //instance 꺼지는 문제
    implementation 'org.springframework.boot:spring-boot-starter-actuator'
    implementation 'org.springframework.cloud:spring-cloud-starter-gateway'
    implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
    runtimeOnly 'io.netty:netty-resolver-dns-native-macos:4.1.76.Final:osx-aarch_64'
}

//instance 꺼지는 문제
dependencyManagement {
    imports {
        mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
    }
}
```

## 🔵 Tryout 4: HikariCP connection pool

### 🔴 Error: HikariCP connection pool attempting to validate database connections that are already closed

It seemed the connection pool is trying to set a network timeout on a connection that is already closed.

<img width="1470" alt="Screenshot 2024-07-10 at 15 55 45" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/7a2b2223-875e-41cc-bdac-4e02ddb710b8">

### 🟠 Cause of problem

- Network issues or database restart
  Don't think this is the cause because network nor db is restarted.
- MaxLifeime Configuration:
  If Configuration of HikariCP is too long,
  connections might stay in the pool for longer than they should,
  causing them be become invalid if database or network state changes.

#### ✔️ update application.yaml

updated the hikari MaxLifetime to 30 minutes in `application.yaml` file.

<img width="456" alt="Screenshot 2024-07-10 at 15 57 41" src="https://github.com/DrugStoreWeb/DrugStore-BE/assets/97790983/915d0494-5cf1-40e7-b95a-791f1bdd62b4">

## 🟢 Solution

Finally, instance is now running without stop. <br>
However, whenever I push, the CICD is not complete and the deployment fails.<br>
Next step is continuous deployment!<br>
