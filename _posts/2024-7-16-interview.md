---
title: Interview practice_drugstore
categories: [Recruit, personal_log]
tags: []
---

<details>
<summary>Click to toggle contents of `code`</summary>

```
CODE!
```

</details>

```Markdown
<details>
<summary>Click to toggle contents of `code`</summary>
    hello

</details>

```

```T
🟠 purpose
🟡 roles of the technology
🟢 implementation steps
🔴 challenges, solutions
🔵 outcomes, benefits
```

## 💡 Technical Questions:

### ✅ Open Market Service Development

- Can you describe the architecture of the open market service you developed for buying and selling cosmetic products?
- What challenges did you face during the development of this service, and how did you overcome them?

### Instance connection lost: JDBC, HikariCP

![IMG_2B08A36D62B9-1](https://github.com/user-attachments/assets/47e010aa-a7ec-44e5-9aef-d724dd2676f2)

```T
🟠 purpose
    - Database connections were staying in the pool for longer than they should
    - resource exhaution
🟡 roles of the technology
1. SWAP
    - extend virtual memory
        - virtual memory: RAM + SWAP space(RAM looks bigger storage that it really has)
    - handle memory overcommitment: paging - move inactive pages to swap
    - prevent OOM errors
        - safety net when system is out of physical RAM
        - graceful degradation
2. version control
3. HikariCP
    - JDBC: Java Database Connectivity
         - connect to database, execute SQL
    - API
    - What is a pool?
    - manages, limits connections
    - What is the diffrence between library vs frameworK? IOC? DI?
    - HikariCP: JDBC connection pool library
  - MaxLifeTime: how long connection can stay in the pool. After MLT, connection closed and removed from pool and recycled.
    - Conection pool?
    - cache of database connections maintained
    - pool manages the connections w the database
    - initialization(create pool of connections) ➡️ connection request ➡️ conection reuse ➡️ connection release
🟢 implementation steps
    - apllication.yaml
🔴 challenges, solutions
🔵 outcomes, benefits
    👍🏻 concurrency control: manage, limit number of connections. resource exhaution ⬇️
    👍🏻 reuse connections, database operation time ⬇️
    👍🏻 scalability
```

#### Too many Connections

```Markdown
🟠 purpose
  - Connection Usage high
  - Connection Miss Rate high
🟡 roles of the technology
🟢 implementation steps
    - mariaDB conf
🔴 challenges, solutions
🔵 outcomes, benefits
  - maximum pool size: max of connections in pool
  - wait_timeout
```

![IMG_3331](https://github.com/user-attachments/assets/28979b93-338b-4bab-a73a-c2f7d1f45366)

### ✅ Jasypt for Data Encryption

- How did you implement Jasypt for encrypting confidential data in your application?

```Markdown
🟠 purpose
    - security of confidential data
🟡 roles of the technology
    - library
🟢 implementation steps
  - gradle based dependencies
  - PBE
🔴 challenges, solutions
    - CICD?
🔵 outcomes, benefits
  - guard Jasypt key
  - minimized the risk of exposure
    👍🏻 env variables reduce
    👍🏻 simplified configuration management
    👍🏻 exposure risk down

```

### ✅ HTTPS

- How did you configure Nginx, SSL, and Route 53 for an HTTPS domain?

```Markdown
🟠 purpose
    - more secure webpage
🟡 roles of the technology
    - Hyper Text Transfer over SSL
    - SSL: certificate
    - Nginx: reverse proxy server
🟢 implementation steps
    - Domain: Gavia
    - Let's Encrypt: CA obtain free SSL cetificate TLS
    - update Nginx config to redirect HTTP to HTTPS.
    - Route 53: made host area to add DNS records to point the domain to our server's IP address.
🔴 challenges, solutions
  - Let's Encrypt: renew certificate for every 90 days, automation
  - 404 error. redirect http to https.
    - create a `symbolic link`, link `config file` to `sites-enabled`
  - 502 error. nginx config, port 443 -> http
🔵 outcomes, benefits
    - cache, load balancing
    - data transfer more secure
```

### ✅ Redis and Gmail SMTP for Email Verification

```Markdown
🟠 purpose
    - Verify valid email, prevent spam
🟡 roles of the technology
    - Redis to save temporary data storage(email verificiation code, 5mins)
🟢 implementation steps
    - Redis: in-memory data storage capability-> fast read, write
        - install on EC2
        - redis config
    - SMTP: reliability, integration with JavaMailAPI easy
🔴 challenges, solutions
    - Trouble: didnt allow firewall, redis conf
🔵 outcomes, benefits
    - fast, efficient handling of verificiation code
    - save memory

```

### ✅ AWS S3 and IAM for Multipart File Uploads

- Can you walk me through the process of using AWS S3 and IAM for uploading multipart files such as images?

```Markdown
🟠 purpose
    - Save images of products, detail page on scalable storage
🟡 roles of the technology
    - Multipart: upload large files in smaller parts(independently & parallel)
    - S3: bucket for storing multipart data
    - IAM: manage access, permission for S3
🟢 implementation steps
    create S3 bucket on AWS
    set correct IAM settings, least previlage principle
🔴 challenges, solutions
    - Trouble: url does not show any image
    - default was private. made get public
🔵 outcomes, benefits
```

- why S3, not DB?

```Markdown
1. scalability(store unlimited, wo performance degradation). DB is not for handling binary services
2. cost effective
3. DBs are optimized for transacional data
4. I/O operation error
```

- What specific IAM policies did you implement to ensure security during file uploads?

```Markdown
  - least privilege principle
  - bucket-policy: allow get, put for just this bucket
```

### ✅ Role-based Functionality

- How did you implement role-based functionality in your application?
- Can you give examples of how the application behavior changes based on different user roles (e.g., seller vs. buyer, user vs. admin)?

```Markdown
1. User has to ask for authorization
2. Seller: register your product, at the price and details you desire
3. Buyer:
```

- buyer posting desired price
- interactive

### ✅ Exception Handling

- resolved real-world challenges in my project.

- What strategies did you use for thorough exception handling concerning stocks, money, and product status?

```Markdown
1. what if there is 0 product left?: sold out exception
2. what if there is less stock than the user wants to buy?: not enough stock exception
3. what if the product is not sold anymore?(product status false): product status exception
4. what if user wants to buy having no money?: no money exception

exception handling was done in all cases
1. Stock management
- sold out exception
- not enough stock exception
- product status exception

2. Financial Transactions
- plus, no money exception
- delete product from cart
```

- Can you provide an example of a complex issue you encountered and how you handled it?

## 💡 Behavioral Questions:

Problem-Solving

Can you describe a time when you encountered a significant technical issue during your project and how you resolved it?
Teamwork

How do you approach working within a team, especially when dealing with complex projects like the open market service you developed?
Adaptability

How do you stay updated with new technologies and tools? Can you provide an example of how you applied a new technology to solve a problem in your project?
Communication

How do you communicate technical details and project progress to non-technical stakeholders?
Project Management

Can you discuss how you manage your time and priorities when working on multiple aspects of a project, such as development, configuration, and handling exceptions?
Scenario-based Questions:
Scaling and Performance

If your open market service experiences a sudden increase in traffic, what steps would you take to ensure it scales effectively and maintains performance?
Security

How would you handle a situation where a security vulnerability is discovered in the data encryption or file upload process of your application?
User Experience

Imagine a scenario where users are reporting slow load times for product images. How would you diagnose and resolve this issue?
Follow-up Questions:
Further Exploration of Technologies

Can you go into more detail about why you chose specific technologies (e.g., Redis, AWS S3) for your project?
How do these technologies work together to support the overall functionality of your application?
Learning and Improvement

What did you learn from this project that you will apply to future projects?
If you were to start this project again, is there anything you would do differently?
