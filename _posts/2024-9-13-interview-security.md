---
title: Interview_cyber security for CV
categories: [Recruit, personal_log]
tags: [interview]
---

```T
🟠 purpose
🟡 roles of the technology
🟢 implementation steps
🔴 challenges, solutions
🔵 outcomes, benefits
```

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

```
- path traversal: access files on web server to which they should not have access
- MariaDB

- IAM:
controlar de forma segura el acceso a los recursos de AWS
quién puede ser autenticado y autorizado para los recursos de RDS
- Jasypt:
- validar la entrada del usuario

- used private IP, resources outside VPC cannot connect
- VPC security group
- CA: validae that the connection is being made to AWS DB, check server certificate
- Password Management

- firewall: called security group in AWS
virtual firewall
control traffic that is allowed to reach, leave resources
control inbound, outbound traffic to EC2
```

</details>

<br>

<details>
<summary> ✅ How would you detect and respond to such an attack in real-time?  </summary>

```

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
```

</details>

<br>

## 📌 Respuesta a Incidente

<details>
<summary> ✅ How would you handle a situation where you detect a potential breach on the web application you developed?  </summary>

```

- confirmar si realmente esta una brecha
- algunas alertas pueden ser falsos positivos o no llegar al nivel de un incidente
- revisar logs: SIEM, WAF
- analysis del alcance, la gravedad, el impacto
- contención
- análisis de incidente
- communicación del incidente
- acuerdo con las leyes de protección de datos, como GDPR
- remediación: parchear, IAM, MFA
- mejora de la seguridad: auditar regularamente, simulaciones de ataques
- documentación del incidente
```

</details>

<br>

<details>
<summary> ✅ What are some alerts that should be considered? </summary>

```
- revisar los logs buscando patrones sospechosos
- múltiples intentos fallidos de autenticación
- solicitudes desde dirreciones IP desconocidos
- actividades fuera de horario normal
```

</details>

<br>

<details>
<summary> ✅ Describe a situation where you had to identify and mitigate a security vulnerability. How did you approach the problem? </summary>

```

```

</details>

<br>

<details>
<summary> ✅ What logs and data would you monitor on a web server to identify security incidents, and how would you correlate that data to detect a potential intrusion?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ How would you use tools like AWS CloudTrail or similar logging systems in your response strategy?  </summary>

```

```

</details>

<br>

## 📌 Encryption, Access Management

<details>
<summary> ✅ What encryption mechanisms did you use in your project, and how did they enhance security?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ Can you discuss the differences between symmetric and asymmetric encryption, and where each would be applicable?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ You’ve worked with AWS IAM for identity management. How would you set up role-based access in a secure way to minimize risk in an enterprise environment?  </summary>

```

```

</details>

<br>

<details>
<summary> ✅ Can you explain the significance of implementing multi-factor authentication (MFA) in your application? What are the typical attack vectors it protects against? </summary>

```

```

</details>

<br>

<details>
<summary> ✅ How did Redis and Gmail SMTP work together in your MFA setup? </summary>

```

```

</details>

<br>

## 📌 Cloud Security and Infrastructure

<details>
<summary> ✅ How did you configure Nginx and Route 53 to enhance the performance and security of your application? </summary>

```

```

</details>

<br>

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
