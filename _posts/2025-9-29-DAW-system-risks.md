---
title: 1.6 Main Security Risks in systems, Cookies
categories: [FP DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Hardware, Software, Firmware, Malware, Ransomware, Openware

- ✔️ **Hardware**: physical components of a system
- ✔️ **Software**: logical components of a system
- ✔️ **Firmware**: very basic software very attatched to hardware, already installed on the hardware that boots automatically(`BIOS`)
- ✔️ **Malware**: software with bad purposes
- ✔️ **Ransomware**: software that kidnaps your computer, blocks your system and asks for money to unblock
- ✔️ **Openware**: opensource software, public software with no license, no copyrights

## ✅ Malware

### 💡 Types of malware

- virus
- worms
- trojan
- spyware
- adware
- keylogger
- dialer
- backdoor

### ☑️ Virus

> software(malware) that enters a system and **auto-replicates**

#### 📌 Two types of virus

- ✔️ **Kernel virus**: attacks the kernel of the OS

- kernel: central block of the operating system
- 😈 can damage process, files, RAM...(everything that the OS)
- can damage the secondary memory and the RAM
- 💊 need to format all the computer, OS, secondary memory...
- ↔️ kernel virus can attack `OS in the secondary memory`

- ✔️ **Macro virus**:

- macro: shortcuts, combination of keys, `ctrl-c`, `ctrl-v`
- macro is a combination of keys to do smth fast, efficiently
- macro virus is activated when you try to use a macro
- when we enable edit in word, we might put ourselves in danger as macro virus can enter
- sometimes word would ask if you want to use macros
- we should becareful when we enable edit, macro, as we can put the computer in risk
- 💊 if you want to enable macro, make sure to enable anti-virus
- 💊 windows come with `window defender`(anti-virus)
- if `windows defender` appears with an exclamation sign ❗️ (`!`), my computer is NOT fully protected
- still, you would be protected from `macro virus`
- if you are also not protected from `macro virus`, you will have a ❌ (`x`)
- ⚠️ if you need to install smth and need to deactivate `windows defender`, only do it for a short time, and do not use macros

- 😈 macro virus can attack an open file, it will attack the **RAM**
- bc open files would be on the RAM
- macro virus will attack the program part of RAM
- macro virus will try to attack the forbidden area of the RAM, which is reserved for the OS
- if macro virus manages to attack the forbidden part of the RAM, your processes will
- ↔️ macro virus can attack `OS in the RAM`

#### 📌 Operating System

- kernel
- operated system is always stored in **secondary memory**
- controls RAM
- controls peripherals: control screen, keyboards, printer
- control files
- control processes
- so if kernel virus attacks the OS, it can damage all things above

- when we switch the computer off, the RAM will be empty

#### 📌 Where files are stored

- when a file is closed, it is stored in the **secondary memory**(harddisk)
- when you double click and it is open, it goes to the **main memory**(RAM)
- inside the RAM that is forbidden to touch of the users, it is only for the OS, called `OS in RAM`

### ☑️ Worms

> tiny simple malware that enters the **RAM** when I execute a program

- goal of worm is to replicate itself, then occupy the complete RAM
- ↔️ the goal of worm is NOT `OS in RAM`

- 😈 RAM is collapsed, cannot open/close any program
- the computer will be frozen
- cannot even turn of the computer
- 💊 strong shutdown, take the electicity off
- there can be hardware damage
- will lose all the content that you did not save

- as worm is saved in the RAM
- when we switch the computer off, the RAM will be empty
- if the computer is turned off, the worm will be gone
- they are dangerous as they collapse the worm,
- but as we can remove them easily by shutting off the computer, relatively easy to remove

- ⚠️ if you detect a worm, do not open any file/program
- do not put anything on the RAM

- 💊 get an anti-virus to detect worms
- 💊 from time to time restart your phone/computer to clean RAM and improve performance

### ☑️ Trojans

> Malware that enters a computer as if it was an innocent file <br>
> Can look like a file that you want/expect to get, so you let it in <br>

- trojans hide in your system
- you will not see anything
- then at the moment you do not have protection, it wakes up
- ↔️ trojans have a **countdown**
- you think "But I didnt connect to internet today. How did it enter?"
- it entered xxx days ago

- 😈 trojans corruts files in the secondary memory(`hard-disk`) next to it
- does not attackt the RAM
- 💊 have to format the computer to erase the secondary memory(`hard-disk`)

### ☑️ Spyware

> Malware that enters the system when we are filling in a form <br>

- steal important information
- 😈 will steal your information, and sell your information to another company
- so that another company can offer you a better product
- ↔️ spyware will not attack your computer
- 👎🏻 spyware doesnt attack computer, but attacks my **privacy**

### ☑️ Adware

> Malware hidden in the banner of an advertisement

- you try to close the advertisement, so you click on `x`
- 😈 but actually banner opens the program ➡️ example of adware
- does not damage the computer
- 👎🏻 not respecting my right to see what I want, my decision making
- I do not want to see the program, but adware opens the program

### ☑️ Keyloggers

> Malware that detects my key strokes

- 😈 steal my password, then sell it to somebody
- 💊 Hashing, salt, pepper can protect against keyloggers

### ☑️ Dialers

> When you dial a free number, you end up getting charged

- when you dial a `free-of-charge` number, (like customer service)
- the dialer can close your call, then opened a `non-free-of-charge` call
- dialer changes `free-of-charge` phone call, to `charging` phone call
- 👎🏻 to you get charged for more phone calls, so that you pay more
- ↔️ will not attack your computer/phone software/hardware

### ☑️ Backdoor

> Malwares that create another alternative IP address(door) for your computer to enter

- antivirus always focuses on the front door
- the backdoor(`alternative IP address`) will be transparent for the antivirus
- so when the backdoor is open, all the malwares can enter
- opens entrance to other malware
- works with another malware, like `backdoor + worm`

## ✅ Ransomware

> blocking/kidnapping my files/program to ask for money

- If a company ransoms you, it will not be hidden
- ransomware will be very evident, to tell you that you have been kidnapped
- then, they will contact you asking for money

#### ❓ How will ransomware make kidnapping evident?

- 1️⃣ Ransomware can corrupt the **metadata**
- your file has different size, name, location, created_date...
- you will not lose the files, but cannot find them, as location has changed
- files are safe, but you cannot reach them

- 2️⃣ Ransomeware can change the **extension** of the file
- all files will be changed into `.lockbit`

#### 💊 What do you do when your company has been ransomized?

- 1️⃣ Contract a company who specialize in ransomware, they will come to see you
- 2️⃣ Try to fix

  - if there is a solution, they can fix
  - if there is no solution, you have to pay

- 3️⃣ If a company has been ransomwared, you need to make it ==public==.

  - ppl might think your company is weak,
  - but the ransomware company will make your security higher
  - so you will be stronger/more secure
  - there is an `honor code` that says, a company that has been ransomwared, if they make it public, will not be ransomwared again
  - so you will not be ransomwared again by another company

  - clients will lose confidence in you, but will stay as you will be stronger
  - ⭐️ you need to inform everyone, even the customers, make it public
  - ⭐️ However, if the company has NOT made the situation public, you should not make it public before
  - in terms of business, the company would want to keep it confidential before they make it public and try to solve it
  - sometimes, they would make you sign a confidence contract

## ✅ Phishing, Smishing, Vishing

- **Phishing**: fake email asking for personal information
- 💊 never introduce your personal information

- **Smishing**: message asking for personal information or for you to click

- **Vishing**: phone calls asking for personal information
- purpose: to know if you are available
- In dark web, there would be a huge data of us, with a tick`/`, checking our availability

## ✅ Rainbow table

> Huge databse in the dark web that contains millions of passwords and hash functions

- 😈 some hackers find the hash function, then share it on the rainbow table
- database contains: 1️⃣ original password 2️⃣ hashing function 3️⃣ encrypted password(hashed result)

- purpose: to enter systems
- they check on the rainbow table, if the system has already has been hacked
- they can use the rainbow table and use it to hack again
- 💊 change password on a monthly basis, maximum monthly

## ✅ Strong attack, Brute Force attack

> Trying repetively with all the possible characters to find your password

- trying to find your password using `loops`
- 💊 nowadays, not used anymore, as we use hashing, salt, pepper

## ✅ Cookies

> file(text) with information about our navigation preferences

### ☑️ Personal cookie

- ⭐️ Normally, cookies are **NOT** security risks
- navigation preferences: the aspect of the webpages
- if you like windows maximized, or half sized, size of characters, if you use darkmore/brightmode
- purpose: to **help** you navigate the way you want

- ⚠️ can be dangerous because some of them keep personal data
- in order to help you, they learn your name/phone number
- there is a law saying `cookies for personal data should be tagged/labeled as personal cookies`
- we could disable them, but we click on `accpet all cookies`

- cookies are saved on the secondary memory(harddisk)
- each user has each own cookie
- one cookie folder **per user**
- one cookie folder **per browser**

```
Q: In a computer with two users and three browsers installed, how many cookies folers do we have?
A: 6
```

- 💊 better to use only one browser regarding cookies

### ☑️ Zombie cookie

- hidden cookies(files) that move from location to location
- keeps references but it's metadata is not permanent/changes every certain time
- file would be in the same place
- but the metadata(name, size, extension, location) keeps changing
- you will not be able to find/locate the file
- 👎🏻 thus, you will not be able to delete the file
- 👎🏻 thus, you cannot use an anti-virus on the file
- 👎🏻 the malware loves attacking these cookie files
- 👎🏻 so in reality, many zombie cookie files are infected, and impossible to clean

- only antivirus programs that are more expensive can path(locate) the zombie cookie files
- 🤷🏻‍♀️ so maybe antivirus companies create the zombie cookie files
- 💊 use a good antivirus program

### ☑️ Session cookie

> cookies that is valid only for that session

- when you logout/switch off, the cookie will be deleted
- only during your session
- reletively safe

### ☑️ Persistent cookie

- the opposite of session cookie
- even when you logout, stays there forever
- will never be deleted
- not very sage

### ☑️ SURE cookie = private cookies

> non personal cookies

- cookie that does not save personal information
- private cookies

```
Q: What cookies should we accept?
A: To be safe, only Sure(private) cookie and session cookies
```
