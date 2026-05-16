---
title: 7.3 Protocols
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

CC by Aru

## ✅ 7.4 Protocols

- Protocols = books or rules for different applications.

### ☑️ Application Layer Protocol Categories

- 1 book for naming things.
- 2 books for IP configuration.
- 3 books for email.
- 2 books for sending attachments.
- 2 books for browsing/navigating the internet.

---

## ✅ DNS (Domain Name System)

- Set of rules for transforming IP addresses into human-readable names.
- Purpose: understand what an IP belongs to.

### ☑️ Example

- `www.google.es`
- `www` = public webpage.
- `google` = company name.
- `.es` = Spanish server/domain.

### ☑️ Important Concepts

- Human-readable name is commonly called a URL.
- More accurately: FQDN (Fully Qualified Domain Name).
- DNS transforms names into technical IPs.
- Example:

  - `https://mail.ef.com`
  - becomes `https://192.2.14.2:25`

### ☑️ DNS Database

- Huge distributed database.
- Different servers manage different domains:

  - `.com`
  - `.org`
  - `.net`

- Solving DNS = converting FQDN into IP address.

### ☑️ FQDN Levels

- Information at the end = more general.
- Information at the beginning = more specific.

#### ✔️ Example

- `mail.ef.com`

  - `.com` = level 1 (general)
  - `ef` = level 2
  - `mail` = level 3 (specific)

---

## ✅ DHCP (Dynamic Host Configuration Protocol)

- Protocol that gives devices an IP address dynamically.
- Used when devices move between networks.

### ☑️ DHCP Server

- Machine that provides IP addresses.
- Connected to database of:

  - free IPs
  - shareable IPs

### ☑️ Server vs Client

- Server = gives something.
- Client = requests/needs something.

### ☑️ DHCP Process (DORA)

#### ✔️ 1. Discover

- Client requests an IP.

#### ✔️ 2. Offer

- Server offers an IP.
- Multiple servers can offer IPs.

#### ✔️ 3. Request

- Client requests one offered IP.
- Usually chooses highest range.

#### ✔️ 4. ACK (Acknowledgement)

- Server confirms assigned IP.

### ☑️ Extra Note

- Another Discover message is sent when signal becomes weak.

---

## ✅ BOOTP (Bootstrap Protocol)

- Gives a temporary IP address.
- Used for remote Operating System installation.

---

## ✅ HTTP (Hypertext Transfer Protocol)

- Protocol used for navigating the internet.

### ☑️ Communication

- Client = computer requesting webpage.
- Server = machine sending webpage.

### ☑️ How HTTP Works

- Client sends request with GET code.
- Server replies with:

  - HTML code
  - HTML version
  - status code

### ☑️ Status Codes

#### ✔️ 1XX

- Not finished, wait.

#### ✔️ 2XX

- OK.

#### ✔️ 3XX

- Request forwarded.

#### ✔️ 4XX

- Bad request/webpage missing.

#### ✔️ 5XX

- Server error.

### ☑️ Important Characteristic

- HTTP has no session memory.
- If error happens, process restarts from beginning.
- Faster browsing usually due to:

  - temporary internet files
  - cookies

---

## ✅ HTTPS (HTTP Secure)

- Secure version of HTTP.

### ☑️ Security

- Uses:

  - public keys
  - private keys
  - PGP (Pretty Good Privacy)

### ☑️ Encryption Idea

- Public key = template/container.
- Private key = password to decrypt content.

### ☑️ Important Notes

- HTTPS prevents interception.
- HTTPS does NOT mean malware-free.
- Many systems besides HTTP use PGP:

  - emails
  - encrypted messaging
  - WhatsApp end-to-end encryption

---

## ✅ FTP (File Transfer Protocol)

- Protocol for sending attachments/files.

### ☑️ TFTP (Trivial FTP)

- Sends file pieces randomly.
- No control mechanism.
- Chaotic and less reliable.

#### ✔️ Example

- Decorative image transfer.

### ☑️ Normal FTP

- Sends file pieces with control.
- Failed transfers restart.
- More reliable than TFTP.

#### ✔️ Example

- Sending school/work files.

### ☑️ FTP Actors

#### ✔️ FTP Client

- Host sending file.

#### ✔️ FTP Server

- Host receiving file.

### ☑️ Ports

- Control ports:

  - 3000
  - 21

- Data ports:

  - client uses ports `>1024`
  - server uses port `20`

### ☑️ FTP Process

#### ✔️ Step 1

- Client port 3000 contacts server port 21.
- Includes client data port `>1024`.

#### ✔️ Step 2

- Server replies ACK.
- Requests confirmation.

#### ✔️ Step 3

- Client replies ACK.
- Double check completed.

#### ✔️ Step 4

- File pieces sent:

  - client `>1024`
  - server `20`

- Every piece needs ACK.

#### ✔️ Step 5

- EOF (End Of File) sent.
- Final confirmation received.

---

## ✅ SFTP (Secure FTP)

- FTP with encryption.
- Uses PGP keys.
- All communication encrypted.

---

## ✅ Emails

### ☑️ Structure

- Header + body.

### ☑️ Header Contains

- From
- To
- Subject
- CC
- CCO

### ☑️ Communication Type

- Asynchronous.
- Receiver may read later.

### ☑️ Email Flow

- Sender sends email to server.
- Server later sends to destination.

### ☑️ Email Protocols

#### ✔️ SMTP

- Sends email from origin to server.

#### ✔️ POP3

- Email removed from server after download.
- Uses port 110.

#### ✔️ IMAP

- Keeps original email on server.
- Destination receives copies.
- Allows multiplatform access.
- Uses port 143.

### ☑️ POP3 vs IMAP

- POP3:

  - cheaper
  - less storage
  - common in governmental systems

- IMAP:

  - modern
  - flexible
  - common in Gmail/Educamadrid

---

## ✅ SMTP Process

### ☑️ Ports

- Uses port 25 on both machines.

### ☑️ Start of Communication

#### ✔️ Message 1

- “hello” → ACK

#### ✔️ Message 2

- “From:” → ACK

#### ✔️ Message 3

- “To:” → ACK

### ☑️ Sending

- Email sent in pieces.

### ☑️ Ending

#### ✔️ Step 1

- Sender says email finished.

#### ✔️ Step 2

- Receiver ACK.

#### ✔️ Step 3

- Sender leaves.

#### ✔️ Step 4

- Receiver ACK.

### ☑️ Important Notes

- Each email generates many messages.
- Attachments use:

  - SMTP for email
  - FTP for file transfer

- Emails consume many resources.
- Avoid unnecessary “thank you” replies in companies.

---

## ✅ Email Actors

### ☑️ MUA (Mail User Agent)

- Final sender and receiver.
- Sending uses port 25.
- Receiving uses:

  - 110
  - 143

### ☑️ MTA (Mail Transfer Agent)

- Transfers email between servers.
- Like a truck carrying packages.

### ☑️ MDA (Mail Delivery Agent)

- Delivers email close to destination.
- Like a mailman.

### ☑️ MAA (Mail Access Agent)

- Rebuilds email from pieces.
- Gives completed email to client.

---

## ✅ SSH (Secure Shell)

- Adds security to insecure communications.
- Provides PGP encryption.

### ☑️ Example

- Emails normally unencrypted.
- SSH adds encryption first.

### ☑️ SSH Process

#### ✔️ Step 1

- Machine 1 requests public key.

#### ✔️ Step 2

- Machine 2 sends public key and requests one.

#### ✔️ Step 3

- Machine 1 sends public key.

#### ✔️ Step 4

- Communication occurs encrypted.

---

## ✅ Proxy-Cache Service

### ☑️ Proxy

- Hides user IP.
- Communications appear from proxy IP.

### ☑️ Cache

- Stores webpage copies locally.
- Avoids repeated internet downloads.
- Saves pages for future access.

### ☑️ If Proxy-Cache Disconnects

- Real IP becomes visible.
- Device always reconnects to internet.
- Temporary web files help future downloads.

---

## ✅ Firewall Service

- Service that opens/closes ports.
- Controls traffic access.

### ☑️ Port Behavior

#### ✔️ Open Port

- Allows data through.

#### ✔️ Closed Port

- Blocks and deletes data.

### ☑️ Examples

- Close port 25:

  - cannot send emails.

- Close port 80:

  - cannot browse internet.

- Close ports 20/21:

  - cannot send attachments.

### ☑️ Company Security

- First machine in company is usually firewall.

---

## ✅ Firewall Zones

### ☑️ MZ (Militarized Zone)

- Protected internal company network.
- Requires login/access permissions.

### ☑️ DMZ (Demilitarized Zone)

- Publicly accessible systems.
- Reachable from internet.

### ☑️ Why Both Are Needed

#### ✔️ DMZ

- Public webpages.
- Marketing services.

#### ✔️ MZ

- Customer/private processes.
- Restricted access.

### ☑️ Working Principle

- Try using DMZ first.
- Move to MZ only when necessary.
