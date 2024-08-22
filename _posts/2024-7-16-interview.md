---
title: Interview practice_drugstore
categories: [Recruit, personal_log]
tags: []
---

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
  - consisten various roles
    - vendedor, comprador, usario, administrador
  - en funcion de cada role
  - permiso
  - productos de cosmetica
- What challenges did you face during the development of this service, and how did you overcome them?

### Instance connection lost: JDBC, HikariCP

![IMG_3332](https://github.com/user-attachments/assets/c49ef48d-d027-4206-badd-c16d1963b431)

```T
🟠 purpose
    - Database connections were staying in the pool for longer than they should
    - resource exhaution
🟡 roles of the technology
1. SWAP
    - extend virtual memory
        - virtual memory: RAM + SWAP space(RAM looks bigger storage that it really has)
    - handle memory overcommitment: paging - move inactive pages to swap
    - allocated 4G of SWAP
    - prevent OOM errors(Out of Memory)
        - safety net when system is out of physical RAM
        - graceful degradation
2. version control
3. HikariCP
    - JDBC: Java Database Connectivity
         - connect to database, execute SQL
    - API?
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

```T
- encontrado
- deplegar
- que se llama
- una instancia en ejecucíon
- host local <-> EC2
- la conexion
- archivo mostraba un error
- errores
- causa
- método HTTP incorrecto/equivocado
- la version no correspondian
- la version encajen

- asignar SWAP
- disco duro, disco solido
- memmoria terminado
- prevenir, evitar(prevent)



- pool: administrar, create, reutilizar, terminar
- permanecer en el pool por mucho tiempo/ muy largo
- empienza a funcionar mal
- de 8h a 30minutos

- para solucionarlo
- con esas tres cosas, he solucionado el problema de instancia perdida
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

- implementar
- encriptar
- datos confidentiales
- libreria
- esta basada en gradle
- encryptacion basada en contraseña
- podia minimizar el riesgo de exposición
- simplificar la gestión de la configuración

- no encontré ningun problema

- objectivo
- desafío
- resultado
- integración
- aleatorio

### ✅ HTTPS

- How did you configure Nginx, SSL, and Route 53 for an HTTPS domain?

```Markdown
🟠 purpose
    - more secure webpage
🟡 roles of the technology
    - Hyper Text Transfer over SSL
    - SSL: certificate(encryption, data integrety, authentication)
    - Nginx: reverse proxy server
🟢 implementation steps
    - Domain: Gavia
    - Let's Encrypt: CA obtain free SSL cetificate TLS, issue a certificate
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

```T
- dominio
- transferencias datos
- transferir datos atraves de la web
- Nginx: redirigir HTTP a HTTPS
- SSL: emitir un certificado
- obtener, obtenido
- añadir registros de DNS
- una Automatización
- instalar
- update: actualizar
- desafío fueron
- válido
- puerto
- mejorado
```

### ✅ Redis and Gmail SMTP for Email Verification

```Markdown
🟠 purpose
    - Verify valid email, prevent spam
🟡 roles of the technology
    - Redis to save temporary data storage(email verificiation code, 5mins)
🟢 implementation steps
    - Redis: in-memory data storage capability -> fast read, write
        - install on EC2
        - redis config
    - SMTP:
        - Simple Mail Transfer Protocol
        - reliability, integration with JavaMailAPI easy
🔴 challenges, solutions
    - Trouble: didnt allow firewall, redis conf
🔵 outcomes, benefits
    - fast, efficient handling of verificiation code
    - save memory

```

```T
- LA PLATAFORMA DE DATOS EN TIEMPO REAL
- era necessario
- la capacidad de almacenamiento
- datos temporales
- confiable
- integracion
- la base de datos
- no quieria que fueran a la carpeta de spam
- efficienete en relacion a los costes
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
  IAM <br>
  > Identity and Access Management

```Markdown
  - least privilege principle
  - bucket-policy: allow get, put for just this bucket
```

```T
- almacenamiento
- Un objeto es un archivo y cualquier metadato que describa ese archivo. Un bucket es un contenedor de objetos
- escalable, escalabilidad
- optimizada datos binarios
- subir objectos en paralelo, individualmente
- administrar permisos
- no podia ver las imagenes
- eso era porque
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

#### Problem-Solving

- Can you describe a time when you encountered a significant technical issue during your project and how you resolved it?

#### Teamwork

- How do you approach working within a team, especially when dealing with complex projects like the open market service you developed?
  - although not my job, helped front end

#### Adaptability

- How do you stay updated with new technologies and tools? Can you provide an example of how you applied a new technology to solve a problem in your project?
  - Swagger V3
    - official document
    - 🔴 CORS error
    - 🔴 Token error
    - 🔴 HTTP error: when using https, need to use APIKEY
    - 🔴 Header name error

#### Communication

- How do you communicate technical details and project progress to non-technical stakeholders?
  - stateless: movie "50 First Dates"

#### Project Management

- Can you discuss how you manage your time and priorities when working on multiple aspects of a project, such as development, configuration, and handling exceptions?
  - Project planning:
    - communication with frontend
    - APIs: request, response
    - ERD
    - configuration
  - Configuration:
    - project manager
  - Development

## 💡 Scenario-based Questions:

#### Scaling and Performance

- If your open market service experiences a sudden increase in traffic, what steps would you take to ensure it scales effectively and maintains performance?
  - concurrency issue

#### Security

- How would you handle a situation where a security vulnerability is discovered in the data encryption or file upload process of your application?
  - rollback git commit

#### User Experience

- Imagine a scenario where users are reporting slow load times for product images. How would you diagnose and resolve this issue?
  - main page loading issue

## 💡 Follow-up Questions:

#### Further Exploration of Technologies

Can you go into more detail about why you chose specific technologies (e.g., Redis, AWS S3) for your project?
How do these technologies work together to support the overall functionality of your application?

#### Learning and Improvement

What did you learn from this project that you will apply to future projects?
If you were to start this project again, is there anything you would do differently?

- main page likes, product differnt DTOs
  logged in? not logged in? check method
