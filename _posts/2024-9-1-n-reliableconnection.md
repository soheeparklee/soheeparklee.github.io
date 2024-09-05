---
title: Reliable Data Transmission
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

How to achieve reliable data transmission over unreliable source/service

## ✅ Packet corruption

- 패킷 손상
- bit error inside packet
- often occur in physical layer

💊 ARQ: retransmit

## ✅ Packet loss

- 패킷 손실
- recieved `bits in packet` lost in lower layers
- 1. packet loss for transmitted packet
- 2. packet loss for response of recieved packet(`ACK`, `NAK`)

## 💊 Countdown timer

- If certain time passes and sender does not recieve `ACK` or `NAK`
- Sender assume that packet is lost, and retranmit packet
  <br>

- How long should sender wait after packet transmission for `ACK` or `NAK`?
- wait more than

  - ➕ sender-reciever travel time
  - ➕ stime for sender to manage recieved packet
    <br>

- if `ACK` is not recieved and timeout, sender will resend
- might result in same packet transmitted more than once
  <br>

- Sender activates countdown timer each time it sends packet
- If certain time passes
- And there is timer interrupt, retransmit packet

## 💊 ARQ

> Automatic Repeat reQuest/Query <br>
> Stop and wait protocol <br>

- 재전송
- error-control protocol
- to automatical retransmission of packets that are corrupted/lost

<br>

- transport layer
- datalink later

<br>

- sender does not recieve acknowledgement before timeout
- implied that packet has been corrupt or lost during transmission
- acccordingly, sender resends the packet

**✔️ Error checking** <br>

- 오류검출
- use checksum to find bit error in packet

**✔️ Reciever feedback** <br>

- 수신자 피드백
- if reciever recieves successfully, send ACK
- if reciever does not recieve, send NAK
- send the `most recent well recieved packet number` with `ACK`

**✔️ Sender retransmit** <br>

- 송신자 재전송
- When sender recieves NAK, retransmit
- Sender will not send more packets until it recieves ACK to the retransmitted packet

<br>
<br>
<br>

- Might happen the reciever's ACK or NAK packet lost/corrupted
- In this case, sender will retransmit(might result in same packet transmitted more than once)
- In ARQ, sender needs to know which packet to send
- and reciever needs to know which packet was recieved
- For distinguishing packets, use **sequence number**

## 1️⃣ Stop and Wait ARQ

<img width="399" alt="Screenshot 2024-09-01 at 17 54 03" src="https://github.com/user-attachments/assets/44a9be62-b1c4-4903-a736-6c07bfda0686">

- sender send one frame at a time
- reciever, if recieved successfully, sends ACK(acknowledgement)
- sender does not send more packets until sender recieves a ACK from the reviever
- sender keeps a copy of the packet
- if sender does not recive before timeout
- sender resends the same packet again
- each timeout is reset after each frame transmission

- 👎🏻 slow, need to wait for reciever ACK

## 📌 Pipelined Protocol

<img width="384" alt="Screenshot 2024-09-01 at 17 54 21" src="https://github.com/user-attachments/assets/ba270b11-75ae-42a3-8d28-29e8895b98b9">

- improves speed in stop and wait ARQ

- send packet without waiting for reciever ACK feedback
- 👎🏻 cannot solve packet loss, corrution issue
- 👎🏻 packet recieved order might be different

## 2️⃣ Go-back-N(GBN) ARQ

- send several packets even **without** receiving ACK from receiver
- GBN sender can send even without reciever replay, maximum `N` packets
- `size N window`(N is decided based on flow-control, congestion-control)
- if reciever does not recive the next number, discard packet
- if reciever recieves successfully, window moves forward
- this process is called **sliding-window-protocol**

✔️ **Sliding Window Protocol**

<img width="390" alt="Screenshot 2024-09-01 at 18 12 19" src="https://github.com/user-attachments/assets/7f5d35d4-d585-4db1-a701-e43a2a0d1b83">

- window size: `N`
- green: transmission complete, recieved ACK
- yellow: did not recieve ACK after transmission
- blue: usable packet, not yet sent
- white: unusable packets
  <br>

<img width="394" alt="Screenshot 2024-09-01 at 21 46 55" src="https://github.com/user-attachments/assets/13c6444f-4669-4b15-9a0e-2621d4bf8ef5">

- window size: 4
- Sender sends packet `0, 1, 2, 3` (window size:4)
- If sender recieves ACK to each packet, window moves forward, sender sends next packets in number order
  - Packet `0` was successfully transmitted, sender recieved ACK, move onto `1, 2, 3, 4`
  - Packet `1` was successfully transmitted, sender recieved ACK, move onto `2, 3, 4, 5`
- Packet `2` is lost.
  <br>
- Reciever keeps track of sequence number of packets
- Reciever recieves `3, 4, 5`, missing `2`
- Thus, reciever throws away `3, 4, 5`
- And send to Sender `ACK1`
- This means, "I have recieved until packet 1. Send me from 2 again"
- Timeout occurs
- Sender has only recieved until `ACK1`, thus sending from packet 2 again, `2, 3, 4, 5`

### 🫱🏻 GBN Sender

**1. Send packet**

- recieve data from higher layer, check if window is full
- if window is full, return data to higher layer, tell window is full(send data later)
- if window is not full, packet created for `next number`, sent to reciever

**2. Recieve ACK**

- When sender recieved `ACK` and `number N` from reciever
- `number N` means packets _until Nth packet_ has been transmitted successfully
- this is called **Cumulative Acknowledgement**
- for example, if sender recieves `ACK 7` from reciever, it means reciever recieved until packet 7 successfully

**3. Timer**

- If packet is lost/corrputed and ACK is `timeout`
- Sender resends `window size N` _number of packets_ starting from ACK N

### 🫲🏻 GBN Reciever

**1. If packet order is correct**

- If packet recived before is number `n-1`
- And packet revieved now is `n`
- Reciever sends `ACK n` to sender
- and sends `packet n` to higher layer

**2. If packet order is wrong**

- Reciever discards the packets with wrong order
- Send ACK with the most recent, well recieved packet number
  <br>
- although discarding the packets seem like waste
- reciever will recieve from sender again(size of window)
- thus, reciever does not have to buffer about wrong order packets
- however, sender has to remember `nextseqnum`

### ☑️ GBN benefits, disadvantages

- 👍🏻 pipelining, more efficient, no waiting time compared to `stop-and-wait ARQ`
- 👎🏻 send packet multiple times, send as much as `window size`
- 👎🏻 if any frame was lost/corrupted, that frame and _the following frames_ will be re-transmitted

## 2️⃣ Selective Repeat(SR) ARQ

- **only** retransmit lost/corrupt packet
- sending process continues even after frame is discovered to be lost/corrput
- 🆚 GBN: Different from GBN, SR does not retransmit `size of window` packets

<img width="387" alt="Screenshot 2024-09-01 at 22 05 33" src="https://github.com/user-attachments/assets/4ab10474-8985-4a7f-926c-4758182bf9b0">

- even if frame is not recieved, sender continues to send the succeeding frames
- until the window is empty
- when process is finished, process continues where it went off

<img width="399" alt="Screenshot 2024-09-01 at 22 07 58" src="https://github.com/user-attachments/assets/1d8976eb-abe6-4699-9386-143f66086ef2">

- window size: 4
- Sender sends packet `0, 1, 2, 3` (window size:4)
- Reciver recieves `0, 1` and `3, 4, 5`
- Reciever did not recieve `2`
- Timeout for packet `2`
- Packet `2` is retransmitted
- Reciever recieves `packet 2` and sends `ACK2` to sender
- now, `packet 2` matches the window `rcv_base`
- Reciever sends `packet 2 and succeeding packets` to higher layer
- Reciever's window slide, now window `6, 7, 8, 9`
- Sender acknowledges that packet 2 has been successfully transmitted with `ACK2`
- Sender window slide
- There can be a point where sender window and reciever window are not identical

### 🫱🏻 SR Sender

**1. Send packet**

- recieve data from higher layer, check if window is full
- if window is full, return data to higher layer, tell window is full(send data later)
- if window is not full, packet created for `next number`, sent to reciever

**2. Recieve ACK**

- If recieve `ACK`, sender checks if `ACK` is on the window
- If on window, check packet as _recieved(green)_
- If the packet number is the _same_ as `window's send_base`
- window slides to the packet with _smallest number, not yet_ `ACK`
- When window slides, if there is _packet not sent(blue)_, send to reciever

**3. Timer**

- Each packet has logic timer
- If packet timer is timout, that packet will be retransmitted

### 🫲🏻 SR Reciever

**1. Recieve packet within `rcv_base ~ rcv_base + N - 1`(within window)**

- If the packet has been recieved for the _first time_,
- save in `recieve buffer`, send `ACK`
- If packet number is `rcv_base`, send succeeding packets to higher layer
- (because packets recieved before could be succeeding `rcv_base`, and could be saved in buffer)

**2. Recieve packet within `rcv_base-N ~ rcv_base - 1`(before window)**

- Send `ACK` even if reciever has sent `ACK` before
- (for window to slide)

### ☑️ SR benefits

- 👍🏻 does not retranmit unnecessary data multiple times

## 📋 Reliable transmission

**✔️ Checksum**

- to discover error in `bit` in `packet`

**✔️ ACK**

- for reciever to notify sender that packet has been recieved successfully
- `ACK5` means until packet 5 has been transmitted successfully

**✔️ NAK**

- for reciever to notify sender that packet has **NOT** been recieved successfully
- send the number of packet that has not been transmitted successfully

**✔️ Sequence number**

- Identify packets with number
- discover missing packet
- discover duplicated packet(same packet sent more than one time)

**✔️ Countdown timer**

- Assume that packet has been lost
- When timeout, retransmit packet
- Could happen that packet is not lost, but timeout(ACK lost, transmission delay)
- Then, same packet sent more than one time could happen

**✔️ Piplelining, Window**

- Sender can send `window size of packets` without waiting for `ACK` from reciever
- Thus, more efficient than `stop-and-wait`
- `window size` will depend on
  - reciever capabilities to recieve, buffer packets
  - network congestion
