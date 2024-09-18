---
title: Interview_cyber security for CV
categories: [Recruit, personal_log]
tags: [interview]
---

## 📌 Web application security

<details>
<summary> ✅ How did you ensure the security of sensitive data in the "Aplicación Web 
```
HTTPS
TLS/SSL
CA: Let's encrypt
Nginx
use symmetric, assymetric key
```
</details>

<br>

✅ Can you explain how HTTPS and SSL/TLS protect data in transit?

```
clave simétrica
```

<details>
<summary> ✅ En el caso de un ataque de recorrido de directorios?  </summary>

- path traversal: access files on web server to which they should not have access
- MariaDB

⭐️ IAM:
controlar de forma segura el acceso a los recursos de AWS
quién puede ser autenticado y autorizado para los recursos de RDS

⭐️ Jasypt:

- validar la entrada del usuario

- used private IP, resources outside VPC cannot connect
- VPC security group
- CA: validae that the connection is being made to AWS DB, check server certificate
- Password Management

- firewall: called security group in AWS
  virtual firewall
  control traffic that is allowed to reach, leave resources
  control inbound, outbound traffic to EC2

</details>

<br>

<details>
<summary> ✅ How would you detect and respond to such an attack in real-time?  </summary>

- un ataque de recorrido de directorios
- enfoque completo y proactivo
- detectar y responder a un ataque

1️⃣ **Detección**

- **1. monitoreo de logs**
- rastrear las solicitudes: monitor requests
- patrón inusual
- 🛠️ WAF, SIEM

- **2. Sistemas de Detección de Intrusiones**
- utilizar herramientas
- configurar reglas para detectar intentos de recorrido de directorios
- generar alertas cuando detecta actividades abnormales

- **3. Firewall de Aplicaciones Web**
- detectar y bloquear solicitudes
- WAF alaizar el tráfico entrante en tiempo real
- bloquear cualquier intento de explotar vulnerabilidades

2️⃣ **Respuesta**

- 1. **Contención inmediata**
- 🛠️ herramientos como WAF, AWS Security Group
- bloquear la dirección IP desde donde se origina el ataque
- evitar

- Si el ataque sigue en curso, restringiría el acceso
- a las partes afectadas

- 2. **Registro y Análisis**
- Revisar los logs
- confirmar el alcance del ataque
- determinar si este ataque es parte de un esfuerzo coordiado más amplio

- 3. **Parcheo y Fortalecimiento**
- aplicar de inmediato los parches
- ajustar las configuraciones

- 4. **Informe y Análisis Forense**
- generar un informe del incidente
- realizar un análisis forense

- 5. **Medidas posteriores al Incidente**
- revisar la arquitectura de seguridad actual
- asegurar las medidas preventivas
- controles de acceso con principio de mínimo privilegio
- evitar que estas vulnerabilidades se repitan en el futuro

</details>

<br>

## 📌 Respuesta a Incidente

<details>
<summary> ✅ How would you handle a situation where you detect a potential breach on the web application you developed?  </summary>

- confirmar si realmente esta una brecha <br>
- algunas alertas pueden ser falsos positivos o no llegar al nivel de un incidente <br>
- revisar logs: SIEM, WAF <br>
- analysis del alcance, la gravedad, el impacto <br>
- contención <br>
- análisis de incidente <br>
- communicación del incidente <br>
- acuerdo con las leyes de protección de datos, como GDPR <br>
- remediación: parchear, IAM, MFA <br>
- mejora de la seguridad: auditar regularamente, simulaciones de ataques <br>
- documentación del incidente <br>

</details>

<br>

<details>
<summary> ✅ What are some alerts that should be considered? </summary>

- revisar los logs buscando patrones sospechosos <br>
- múltiples intentos fallidos de autenticación <br>
- solicitudes desde dirreciones IP desconocidos <br>
- actividades fuera de horario normal <br>
- intentos acceder archivos que neccessita mas previlegio <br>
- IP blacklist <br>

</details>

<br>

⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️

<details>
<summary> ✅ Describe una situación en la que tuviste que identificar y mitigar una vulnerabilidad de seguridad. ¿Cómo abordaste el problema? </summary>

- trabajé <br>
- durante una revisión rutinaria de seguridad <br>
- utilicé OWASP ZAP para escanear los vulnerabilidades <br>
- identifiqué una vulnerabilidad de inyección SQL <br>
- manipular las consultas de la base de datos <br>
- acceder a información sensible <br>
  <br>
- validación y saneamiento de entradas <br>
  - consultas como delete, 1=1 <br>
- colaboración con el equipo de desarrollo <br>
  - explicar la vulnerabilidad y cómo prevenir <br>
  - frontend tmabien revisado la vulnerabilidad <br>

<br>
- resulado mitigar la vulnerabilidad, mejorar las prácticas de desarrollo <br>

</details>

<br>

<details>
<summary> ✅ ¿Qué logs y datos monitorearías en un servidor web para identificar incidentes de seguridad, y cómo correlacionarías esos datos para detectar una posible intrusión? </summary>

- logs de acceso de servidor web: patrones abnoramales, IP de origen, intentos a acceder a archives <br>
- logs de error: fallos repetidos al acceder <br>
- logs de authenticación<br>
- logs de WAF: identificar, bloquear intentos malintencionado, XXS, reconocimiento<br>
- logs de redes: syslog <br>
- origin de la dirreciones de IP: comparar IPs de acceso con listas de amenazas conocidas(blacklist)
- sistema de detección de intrusiones <br>

</details>

<br>

<details>
<summary> ✅ How would you use tools like AWS CloudTrail or similar logging systems in your response strategy?  </summary>

⭐️ CloudTrail

- logs
- content type
- location
- typo de solicitude

</details>

<br>

## 📌 Encryption, Access Management

<details>
<summary> ✅ ¿Qué mecanismos de cifrado utilizaste en tu proyecto y cómo mejoraron la seguridad?  </summary>

⭐️ Jasypt <br>

- cifrar variables ambientales<br>
- MD5<br>
  - algoritmo hash<br>
  - no requerir reversibilidad<br>
- DES(Data Encrpytion Standard)<br>
- cifrado simmétrico<br>
  <br>

⭐️ JWT <br>

- HS256(HMAC-SHA256) <br>
- en la generación y validación de JWTs <br>
- garantizar la integridad authenticidad de los tokens <br>
- asegurar autenticaión <br>

</details>

<br>

<details>
<summary> ✅ Can you discuss the differences between symmetric and asymmetric encryption, and where each would be applicable?  </summary>

⭐️ simétrico <br>
<br>

- utilizar una sola clave<br>
- 👍🏻 Ventajas: mas rápido<br>
- 👍🏻 Ventajas: requiere menos potencia computacional<br>
- 👎🏻 Desventajas: el intercambio seguro de la calve<br>
- 🛠️ Aplicaciones: cifrar discos, bases de datos<br>
- 🛠️ Aplicaciones: communicaciones internas<br>
- 🛠️ AES, DES<br>

⭐️ asimétrico<br>
<br>

- clave pública, clave privada <br>
- cifrar: clave pública <br>
- descifrar: clave privada <br>
- solo propietario de la clave privada puede descifrar <br>
  <br>
- 👍🏻 Ventajas: solucionar el problema del intercambio de claves <br>
- 👎🏻 Desventajas: mas lento <br>
- 🛠️ Aplicaciones: TLS, SSL <br>
- 🛠️ Aplicaciones: firmas digitales <br>
- 🛠️ RSA, diffie hellman, ECC <br>

</details>

<br>

<details>
<summary> ✅ Has trabajado con AWS IAM para la gestión de identidades. ¿Cómo configurarías el acceso basado en roles de manera segura para minimizar riesgos en un entorno empresarial? </summary>

- controlar acceso de AWS recursos
- authenticar, authorizar
- minimo previlegio

- basado en roles
- grupos de IAM: programmador, usario
- solo usarios con role programmador puede acceder

- crear roles separados para servicios y usarios
- una instancia de EC2 necesita acceso a S3, asignado un rol de IAM para EC2
- con permisos de acceso bucket S3

- permitir que una EC2 instancia acceda a un S3 bucket(depósito S3)
- documentado JSON definir roles, aciones permitido, denegado

</details>

<br>

<details>
<summary> ✅ Que es "el principio de menor privilegio" ? </summary>

- otorgar solo los permitos estrictamente necesarios para realizar sus tareas
- (grant)
- limitar acciones, recursos que necesita

</details>

<br>

<details>
<summary> ✅ Puedes explicar la importancia de implementar autenticación multifactor (MFA) en tu aplicación? ¿Contra qué vectores de ataque típicos protege? </summary>

- require dos o más formas deverificaión para authenticación
- una cosa que el usario sabe, tiene, hace, es, o el ubicación de usario
- fortalezar la seguridad de acceder
- reducir el risego de acceso no autorixado

- robo de contraseñas
- ataques de keyloggers
- ataques de fuerza bruta

</details>

<br>

<details>
<summary> ✅ How did Redis and Gmail SMTP work together in your MFA setup? </summary>

- proceso de verificación en dos pasos

1. contraseña
2. código de un solo uso (OTP) se envía por correo electrónico

⭐️ Gmail SMTP

- enviar el código temporal

⭐️ Redis

- almacenar(store) temporalmente el OTP
- generar el cógido, guardar en Redis con un tiempo de expiración corto(5 min)

- 👍🏻 velocidad
- 👍🏻 capacidad de manejar datos temporales

1. Generar OTP único
2. El OTP almacena temporalmente en Redis
3. El OTP se envia al correo electronico del usario utilizando SMTP
4. Usario recibe el OTP
5. Usario ingresa el código
6. Verficiar el código ingresado
7. Si es correcto y no ha expirado, el usario puede acceder

</details>

<br>

## 📌 Cloud Security and Infrastructure

<details>
<summary> ✅ How did you configure Nginx and Route 53 to enhance the performance and security of your application? </summary>

⭐️ Nginx

- servidor proxy inverso
- configuración de HTTPS con TLS/SSL: certificado de SSL/TLS
- redirigir(redirección) HTTP a HTTPS
- cashing

⭐️ Route53

- configurar el servicio DNS
- manejar el nombre de dominio
- drugstore.shop

- mejorar rendimiento(performance)
- velocidadven actualizar productos
- optimizar el enrutamiento

</details>

<br>

✅ Ventajas de HTTPS

- proteger los datos sensibles
- evitar ataques de intermediarios

<details>
<summary> ✅ Can you explain the importance of DNS security, and how misconfigurations could lead to vulnerabilities?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ What are some best practices you followed when working with AWS S3 for secure file storage and access control?  </summary>

```

```

</details>

<br>

## 📌 Threat detection and Mitigation

<details>
<summary> ✅ If your web application was under a Distributed Denial of Service (DDoS) attack, how would you detect it, and what measures would you take to mitigate it?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ How would you implement security measures to prevent cross-site scripting (XSS) and SQL injection attacks in your web application? </summary>

```

```

</details>

<br>

## 📌 General cybersecurity knowledge

<details>
<summary> ✅ As a member of a blue team, how would you collaborate with other teams (e.g., red team, IT, DevOps) to improve the security posture of an organization?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ What are the most common types of attacks a blue team is responsible for defending against in a cloud-based environment?

  </summary>

```

```

</details>

<br>

## 📌 Industry Specific

<details>
<summary> ✅ Deloitte emphasizes robust incident response frameworks. How would you contribute to an effective incident response team based on your experience?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ Cybersecurity is evolving constantly. How do you keep yourself updated with the latest security trends and vulnerabilities?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ Can you walk me through how you would configure a firewall to block malicious IPs based on your experience? </summary>

```

```

</details>

<br>

<details>
<summary> ✅ What factors would you consider when creating firewall rules to balance security and usability?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ What tools or platforms have you used to perform vulnerability scanning on a web application, and how do you prioritize which vulnerabilities to address first?  </summary>

```
OSWAP ZAP
SQL injeciton
```

</details>

<br>

- con que frequencia ~ : how often

## 📌 Database security

- La retención: 7 días de retención de datos
- data retention: RDS free tier 7 days
- rolling window of data history

## 📌 Trouble Shooting, Mejorar

✅ Too long to get main page

✅ Instance connection lost

- IP address

<details>
<summary> ✅  </summary>

```

```

</details>

<br>

<details>
<summary> ✅   </summary>

```

```

</details>

<br>

<details>
<summary> ✅   </summary>

```

```

</details>

<br>

<details>
<summary> ✅  </summary>

```

```

</details>

<br>
