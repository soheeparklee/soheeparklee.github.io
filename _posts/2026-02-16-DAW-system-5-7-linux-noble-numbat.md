---
title: 5.7 Installation of Ubuntu
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Installation on RM

[![Screenshot-2026-02-16-at-17-45-34.png](https://i.postimg.cc/JnGX5nPQ/Screenshot-2026-02-16-at-17-45-34.png)](https://postimg.cc/MMJXWWkc)

## ✅ Installation on VM

- ☑️ Suggestion 1
- Internal harddisk in order to avoid slow reading/writing access to USB

- ☑️ Suggestion 2
- The `iso` for the Ubuntu in the VM
- should be inside the `downloads` folder(internal disk) ⭕️
- never install `iso` from the external disk ❌
- if you put `iso` from the USB, it will take a long time

[![Screenshot-2026-02-16-at-17-54-04.png](https://i.postimg.cc/7YCBZP4C/Screenshot-2026-02-16-at-17-54-04.png)](https://postimg.cc/Whvm9vhj)

## ✅ Incidents that can happen while installing Ubuntu on VM

- 😱 **Incident: does not install**
- If ubuntu does not install
- disable the `SVGA`
- or disable the `3D`
- in order to weaken the VM

[![Screenshot-2026-02-16-at-17-45-06.png](https://i.postimg.cc/3Jpgqk7v/Screenshot-2026-02-16-at-17-45-06.png)](https://postimg.cc/PPXpprCX)

- 😱 **Incident: the screen is frozen**
- ⭐️ Invalid settings: sometimes it is needed
- when after installing linux, the screen stays frozen
- deactivate `3D` and `SVGA`

```
❓ Why does iso work in my computer but not in carlos's computer?
bc iso is a seed
```

- 😱 **Incident: button does not appear**
- even if you have `SVGA`,
- the continue button might not appear
- 💊 click on `tab`, then click on `enter key`

- 😱 **Incident:**
- everything is installed,
- but the next day, the machine does not boot
- ❓ why does this happen? we gave the required minimum RAM
- 💊 give more RAM

- 😱 **Incident: mouse disappears**
- after when everything is installed, mouse disappears
- ❓ why does this happen? not enough graphic power
- 💊 enable `3D acceleration`, enable `SVGA`
- mouse only work when minimum requirements are satisfied
- so before installing, maybe disable `3D acceleration` and `SVGA`
- then after installing, if mouse is gone, enable `3D acceleration` and `SVGA`

- 😱 **Incident: Missing booting system**
- the `.iso` file is missing
- `.iso` should be added to the `almacenamiento > IDE`

- 😱 **Incident: Not fatal error**
- when the shared folder, the USB was entered last time,
- but now the VM cannot find it
- so when we have created shared folders
- but they cannot get activated bc we forgot to insert the USB
- 💊 `accept the error` or `insert the USB`
- if the USB that you insert today is different from the old one
- 1️⃣ If the USB has changed its letter, no problem
- 2️⃣ but if the USB has changed its letter,
- you will have to delete the old shared folder
- and add the new USB as a shared folder

- 😱 **Incident: Graphic interferences**
- it happens bc of the 2D graphic problems
- this problem is not bc of 3D
- controller is also `VMSVGA`, which is also correct
- 💊 when you have 2D issue, give more video RAM to the VM

- 💡 Note:
- same `.iso` can behave differently depending on the host

## 💡 Summary

- for installing modern linux in limited computers

- 1️⃣ creating VM
- `3D acceleration` ⭕️
- `VMSVGA` ⭕️
- half of `Video RAM`

- 2️⃣ Installing ubuntu `.iso`
- `3D acceleration` ❌
- `VMSVGA` ❌
- we need to weaken the VM

- 3️⃣ Use ubuntu, but mouse disappears
- `3D acceleration` ⭕️
- `VMSVGA` ⭕️

## ✅ The installation process is automatic

- should run automatically
- but sometimes it does not
- and you have to click on a button with a red star
- this button is for installing
- click on the button and install Ubuntu

## 📌 How to install ubuntu(step 1~9)

**(1) language: choose english**

[![2-language.png](https://i.postimg.cc/CKtkMrwn/2-language.png)](https://postimg.cc/zLCV0jbq)

**(2) accessiblity: for users with difficulty, issues**

[![3-accessibility.png](https://i.postimg.cc/fy79KwmJ/3-accessibility.png)](https://postimg.cc/30RNrQLT)

**(3) keymap: always try your keyboard, try to enter smth**

[![4-keymap.png](https://i.postimg.cc/L6Rfs1Fj/4-keymap.png)](https://postimg.cc/BtYtYt6v)

**(4) internet connection:**

[![5-internet.png](https://i.postimg.cc/sgHZKHQm/5-internet.png)](https://postimg.cc/G4Y2mQjT)

- internet connetion is recommended for updates,
- do not use `do not connnect` ❌

**(5) choose if you want `Live Ubtuntu` ot `install Ubuntu`**

[![6-live-Install.png](https://i.postimg.cc/QCjtjcK3/6-live-Install.png)](https://postimg.cc/JDdmqDQ6)

- `Try Ubuntu`: means `Live`, do not install, but nothing is saved

**(6) choose interactive ⭕️ never automatic installation ❌**

[![7-interactive.png](https://i.postimg.cc/vHqBdgY1/7-interactive.png)](https://postimg.cc/QH7sQMWs)

- automatic is creating partitions by default
- if you choose automatic, linux will create only one partition `\(root)`
- we want distro hopping, swap...so no automatic ❌

**(7) which apps to start with? choose defualt ⭕️ never extended ❌**

[![8-apps.png](https://i.postimg.cc/50V9m837/8-apps.png)](https://postimg.cc/VSKcfr2n)

- extended will put all sorts of apps you do not need

**(8) Third party screen**

[![9-third-Party.png](https://i.postimg.cc/Kj9ZFwyf/9-third-Party.png)](https://postimg.cc/0Kwg0tjK)

- do not install any third party applications
- unless you are explicitly told to do so

**(9) Type of installation: erase ❌ manual installation ⭕️**

[![10-installation.png](https://i.postimg.cc/kXpnp0s5/10-installation.png)](https://postimg.cc/tYFQ1mL0)

- `option erase`: is the same as automatic installation, creating only one partition
- choose `manual installation`

## ✅ Create partitions in Ubuntu

[![11-gnome4.png](https://i.postimg.cc/MKNSDyZV/11-gnome4.png)](https://postimg.cc/gnVQcLZ2)

- **(1) after choosing manual, enter `GNOME4`**
- `GNOME4`: `GPartEd` modified for `Ubuntu`

- in `GNOME4`, you do not have to choose `MBR` or `GPT`
- bc `GNOME4` detects automatically what you need
- depending on the BIOS

- **(2) click on plus to create new partitions**

[![12-plus.png](https://i.postimg.cc/mrNWBJYK/12-plus.png)](https://postimg.cc/nszP1dw1)

- **(3) Ubuntu needs 25GB**
- recommend `10GB for data(home)` and `15GB for the kernel`

#### ☑️ `/root`

[![13-practica-partition-root.png](https://i.postimg.cc/SKG3w84D/13-practica-partition-root.png)](https://postimg.cc/Z9CwNWCd)

- `15GB`
- `ext4`
- `Mount point`: `/`

```
What is mounting in Linux?
- we had to click "automontar" for USBs

✔️ In Linux,
    - partitions,
    - devices(camera),
    - drivers...
    - everything
- is only useable/accessible when it is denominated,
- when it has a nickname

✔️ Mountpoint: nickname for that
- without a mountpoint, you cannot use/access it in Linux

✔️ Mountpoints are predefined
/ : mandatory mountpoint of the kernel
/boot : for booting
/home : for data
/tmp : standard mountpoints for folders that you dedicate to temporal files
```

#### ☑️ `/boot/efi`

[![14-partition-efi.png](https://i.postimg.cc/4yY07ScZ/14-partition-efi.png)](https://postimg.cc/p5tC3kk1)

- will be created automatically
- bc we clicked on `efi` while creating VM
- more or less `1GB` will be allocated
- `FAT32`: same as `efi` system

#### ☑️ `/boot`

[![15-practica-partition-boot.png](https://i.postimg.cc/g2VTZRx2/15-practica-partition-boot.png)](https://postimg.cc/w1B2K15C)

- `500MB`
- `ext4`
- `Mount point`: `/boot`
- also would be possible with `300MB`,
- but as this machine is only for `Linux`, you can make it bigger

#### ☑️ `/swap`

[![16-practica-partition-swap.png](https://i.postimg.cc/T2ZxjV3c/16-practica-partition-swap.png)](https://postimg.cc/7bMjwT7C)

- create the SWAP first, then create the `/home`

- our RAM is `4GB`
- so swap also `4GB`
- partition: `used as SWAP`
- ⭐️ no `Mount point` for SWAP

#### ☑️ `/home`

[![17-practica-partition-home.png](https://i.postimg.cc/C1Ryk5yH/17-practica-partition-home.png)](https://postimg.cc/WFcfP21h)

- create the SWAP first, then create the `/home`
- normally, `/home` is left until the end
- so that it can have all the remaining space after allocating the SWAP

- all the left space `11125MB`
- `ext4`
- `/home`
- free space is totally until you format it

#### ☑️ final

[![18-practica-partition.png](https://i.postimg.cc/wT8KR9wn/18-practica-partition.png)](https://postimg.cc/6T0bDxJh)

#### 💡 GRUB

- 1️⃣ if we have efi
- `GRUB` will be automatically stored in `/boot/efi`
- 2️⃣ if we had lecagy BIOS
- if we didnt click efi,
- then `GRUB` will be stored in `/boot`

[![19-grub.png](https://i.postimg.cc/g001bj2f/19-grub.png)](https://postimg.cc/87qZh1WH)

- we need to confirm that the `GRUB` willl be installed
- in the same disk as `/boot/efi`
- as `/boot/efi` is `sda2`, the disk that it will be stored is `sda`
- so, `GRUB` will be stored in `sda`

## 📌 continue installing Ubuntu...(step 10~16)

[![20-user.png](https://i.postimg.cc/0j7B0JVF/20-user.png)](https://postimg.cc/wRT2638Q)

**(10) Your full name**

- name of the installer
- not technical name ❌
- recommdended: your initials in capital letters
- 👀 SHPL

✔️ **Concept of super user**

- the `installer` is an `administrator`
- ⚠️ but, NOT the `super user`
- `super user` is the `root user`, known as `su`
- and `super user` is not a phisical user, its a virtual user
- the `super user` has all the permissions
- `super user` can even distroy the `administrator`

- you can take the role of the `super user` if you want
- ⚠️ But not recommended
- better to be `not super user`
- and ask the `super user` to do things for you
- 👉🏻 use `sudo...` to do things that I do not have permissions for

**(11) computer name**

- `my name from above in lower letters` - `name of computer`
- in VM, name of computer is `VirtualBox`
- do not modify, leave as default
- 👀 `shpl-VirtualBox`

**(12) user name = technical name**

- for login
- same as full name, but not capital
- this is the technical name
- do not modify, leave as default
- 👀 `shpl`

**(13) password**

[![21-password.png](https://i.postimg.cc/zD9LLRm6/21-password.png)](https://postimg.cc/XXkNmqYk)

- in the initial installation,
- it is typical to choose as inital password as same as logging
- so same as technical name
- 👀 `shpl`
- check `Require my password to log in`

**(14) Do not tick `Use Active Directory`**

**(15) Choose timezone**

[![23-timezone.png](https://i.postimg.cc/vBCm6CK4/23-timezone.png)](https://postimg.cc/cgMWpk0W)

- modify it to my timezone

**(16) final page**

[![23-timezone.png](https://i.postimg.cc/vBCm6CK4/23-timezone.png)](https://postimg.cc/cgMWpk0W)

- never switch the VM off now
- `save state`: frozen ➡️ big error
- you can only use `save state`
- after the message `installing the system`
- freezing the machine now can break the machine
- when the `installing the system` message is over, then you can freeze

[![25-frozen.png](https://i.postimg.cc/jdHjLg42/25-frozen.png)](https://postimg.cc/4m3G01MR)

- and after finishing installation
- mandatory to `restart`

[![26-finish.png](https://i.postimg.cc/0QKkxcNy/26-finish.png)](https://postimg.cc/mzRfy3Mv)

- when when you `restart`
- it is mandatory to extract the `iso`

- when you restart,
- you will see the full name `SHPL`
- the technical name is secure, will never be shown

- when you fill in your password,
- then press enter

## 💡 Graphical issues solution summany

[![Screenshot-2026-03-02-at-15-23-26.png](https://i.postimg.cc/Dw08Sr9W/Screenshot-2026-03-02-at-15-23-26.png)](https://postimg.cc/TK8RSDYG)

- for initial setting use `VMSVGA` and `3D`
- if there is a problem with VM installation, and your windows do not appear use `VBoxVGA` and eliminate `3D`
- if the mouse disappears, use `VBoxSVGA` or `VMSVGA` and `3D`
- 👉🏻 you can `toggle` the settings, when they do not have a fixed solution
- toggle: setting that is not stable, has to be modified depending on the situation

```
❓ Explain how the graphic toggle works in Ubuntu
- when you first install, use VMSVGA and 3D
- if there is a problem with VM installation, modify the settings to VBoxVGA and disable 3D
- if the mouse disappears, you should use VBoxSVGA or change back to VMSVGA and 3D
```

## ✅ Important steps after the first login

**(1) Welcome page**

**(2) Ubuntu Pro: Ubuntu with lots of extra in** `/opt`

- do not upgrade now, skip

**(3) Improve ubuntu**

- two ways of making community improve
  - (1) not sharing
  - (2) sharing only basic feedback: all the `/sys` errors are sent to the Linux company canonical
  - (3) sharing all feedback:
  - if we share all the feedback, all the `/sys`, `/prof` will be sent to canonical
  - in windows, share only basic feedback
  - in linux, good practice to share everything

**(4) GNOME flavor**

- Ubuntu 24 has `GNOME 4.6`
- the apps button is a circle now

- The first thing that the technician has to do
- is search the command terminal
- and add to favorites

#### ✔️ **Pin the terminal**

[![27-terminal.png](https://i.postimg.cc/BQ0S9597/27-terminal.png)](https://postimg.cc/dD5PGy0G)

- click on apps
- search terminal
- right click, pin to dash

- when we run in terminal
- 🟰 it means we are running it in the shell
- 🟰 which means, all the commands are checked by `super user`

- 🆚 if we run outside the terminal
- by using visual buttons,
- this is for standard users
- these buttons are not shell protected ❌
- buttons have many less functionalities, for standard users

- visual buttons require graphic power
- 🆚 but the terminal does not require graphic power
- 🟰 the terminal will always work, even when graphic resources are limited

✔️ **The terminal has level 0**

- the terminal has a `run level 0`: top priority
- so linux always gurarantees
- even when all graphics, buttons fail
- the terminal will work

- If we stop all the run levels greater than 0,
- when you are paralyzing all the buttons
- which means you can only use the terminal
- which means you are limiting the use to only technitians
- and limiting standard users

#### ✔️ **BASH**

> Bowne Again SHELL

- Bowne: best friend of Linux
- in every linux, the command shell is normally named after a person

#### ✔️ **Prompt**

[![28-prompt.png](https://i.postimg.cc/DwCnXtJq/28-prompt.png)](https://postimg.cc/xXbwrpPC)

- the commands line is called `prompt`

- `technical name` @ `computer name` : `my directory` $

`shpl@shpl-VirtualBox:~$`

- `shpl`: technical name
- `VirtualBox`: computer name
- `~`: my personal folder, my portion in `/home`
- `$`: if I am not superuser
- `#`: if I am useruser

- 👀 `shpl@shpl-VirtualBox:~$`
- means I have logged in as shpl
- who am I? shpl
- I am connected to machine VirtualBox
- I am located in `/home/shpl`
- and I am not a super user

- 👀 `root@MERCURY:/root#`
- I am super user
- I am connected machined called MERCURY
- I am in `/root`, which is my personal folder as super user

- ⚠️ If you see `#`, logout

## 📌 Guest Addtions installation

- once the VM OS is istalled
- we should install GA
- two ways of installing GA `(1) graphic mode` and `(2) command mode`
- command mode is recommended
  - as graphic mode requires a lots of graphic
  - so only follow graphic mode when you do not have graphic issues
  - and you can give lots of graphic resources
  - VRAM 256MB

```
❓ Why did you install GA in command mode?
- bc we have to give VRAM of 256MB and we cannot
```

#### ☑️ Install GA in command mode

**(1) Devices > insert guest additions**

- when you click it, a CD should appear

[![2ga1.png](https://i.postimg.cc/q7S45Dxm/2ga1.png)](https://postimg.cc/LqtcqT7f)

**(2) Write down GA version**

- the version of the guest addition we are installing might change
- bc the GA depends on the `iso`
- so you should keep recrod of the guest addtition
- ⚠️ this is case sensitive ⚠️
- 👀 `VBox_GAs_7.1.10`

[![2ga2.png](https://i.postimg.cc/BQ4skKHg/2ga2.png)](https://postimg.cc/YjnJmjXG)

**(3) Where is my GA?**

- In which folder the information of CDs are stored?
- CDs and USBs are linked in `/media`
- inside the `/media`, there is a `folder for my user`
- 👀 and inside the `user folder`, the CD will be located
- `/media/shpl/VBox_GAs_7.1.10`

**(4) Execute in terminal, run application**

[![Screenshot-2026-03-02-at-15-43-54.png](https://i.postimg.cc/5y7dFCzQ/Screenshot-2026-03-02-at-15-43-54.png)](https://postimg.cc/1VqYk4Jy)

- then execute from that CD you have inserted
- inside the folder `/media/shpl/VBox_GAs_7.1.10`
- the application named `VBoxLinuxAdditions.run`
- you need administration permissions
- 👉🏻 use `sudo` and ‼️ add one spacebar ‼️
- run `sudo /media/shpl/VBox_GAs_7.1.10/VBoxLinuxAdditions.run`

[![2ga4final.png](https://i.postimg.cc/TYwNK26W/2ga4final.png)](https://postimg.cc/s1k48r1V)

- and everytime you run `sudo`,
- it will ask your password
- type for password

**(5) 🔴 Will see error packages not included**

[![2ga5.png](https://i.postimg.cc/W38S4CYW/2ga5.png)](https://postimg.cc/627CjjXn)

- there are two packages that you need
- but that are not included in the GA
- the two packages are

  - `bzip2`
  - `tar`
  - these two packages are necessary to decompress the GA
  - for unzipping the GA

- 💊 to install two packages
- run `sudo apt install bzip2 tar`
- `apt` is a package of installers
- ‼️ internet connecetion is neccessary

```
❓ Why cannot I install the packages?
- bc you do not have internet
```

- ❓ What happens if there is no internet connection?

  [![Screenshot-2026-03-02-at-15-54-39.png](https://i.postimg.cc/rw6cG5bv/Screenshot-2026-03-02-at-15-54-39.png)](https://postimg.cc/PPMBTvd4)

- If there is not enough IPs
- 💊 change to NAT, do not use bridge

- `apt -get` is also possible for installing things
- but old fashioned

**(6) 🔴 But even after installing the packages, you might get an extra error**

[![2ga6.png](https://i.postimg.cc/tCYDXr3N/2ga6.png)](https://postimg.cc/Whc08wfd)

- 🔴 the extra error: `gcc make perl packages missing`
- means the kernel modules are missing

- the `perl, make, gcc` is for creating link
- between my kernel and the users servers of the hybrid OS
- hybrid OS has `kernel + user services(extra commands for extra things)`
- in order to make users servers work
- we need three packages
- `gcc`
- `make`
- `perl`
- 👉🏻 These three packages are called `Kernel modules`

- 💊 install `sudo apt install gcc make perl`

[![Screenshot-2026-03-02-at-16-00-29.png](https://i.postimg.cc/htwCQ05v/Screenshot-2026-03-02-at-16-00-29.png)](https://postimg.cc/7531pSDr)

- even if you had it installed
- you can install again
- no problem

**(7) if you have Error with `E`(optional)**

- 🔴 If you get an error starting with an `E`

- it means you have a weak internet connection
- 💊 use stronger internet
- 💊 or download it in another place
- 💊 change to NAT

- or the need of updating your system
- 💊 update using commands from step 8

**(8) After installing smth, update**

[![2ga7.png](https://i.postimg.cc/XJYdsJxg/2ga7.png)](https://postimg.cc/gw1xJGCw)

[![2ga8.png](https://i.postimg.cc/Rh3fzDkJ/2ga8.png)](https://postimg.cc/gLWrVNkG)

- `sudo apt update`
- `sudo apt upgrade`
- link perfectly all the commands you have just ran

## 💡 Summary of installing missing packages

- `sudo apt install bzip2 tar`
- `sudo apt install gcc make perl`

- `bzip tar` is for decompressing GA
- `gcc make perl` is for linking to the kernel
- when we download the GA
- we download basic version in kernel
- then we download optional repositories

- then after installing
- run `update` and `upgrade`
- `update` and `upgrade` create link/dependencies between commands

## 📌 continue Guest Addtions installation...

**(8) restart/reboot the system**

- sometimes you get a reminder to restart
- but after installing everything, just restart
- `sudo reboot`

**(9) Now, retry the installation of the GA**

- sometimes you have to install two times
- bc of missing dependencies/links

[![2ga9.png](https://i.postimg.cc/g0YZ0JC8/2ga9.png)](https://postimg.cc/HrhxZpsk)

**(10) test 1: Test GA**

```
GA can do three things
- Host + F
- shared folders for USB between VM and RM
- Bidirectional
```

- with `Host+F`, maximize the window
- and make screenshot with `Host+E`

- full screen with `Host+F`

[![Virtual-Box-DW1E-Ubuntu24-04-4LTS-Noble-Numbat-So-Hee-Park-02-03-2026-practica.png](https://i.postimg.cc/jqXdscxb/Virtual-Box-DW1E-Ubuntu24-04-4LTS-Noble-Numbat-So-Hee-Park-02-03-2026-practica.png)](https://postimg.cc/YjvwR1Ln)

- 🔴 if when taking screenshot, the screen blinks, and gives you problems
- 💊 then give more Video RAM
- if not possible, you already gave maximum Video RAM
- change the graphical controller
- most probably, downgrade the graphic controller, without `S`

**(11) test 2-1: Test shared folders**

[![2ga11.png](https://i.postimg.cc/KzTkqMBh/2ga11.png)](https://postimg.cc/LYH8hhxx)

- you need to have USB that is considered a shared folder

- In linux to use shared folders
- you need to add your user to the group of users who can share folders
- 👀 If you want to play video games, you need to add your user to the group of users who can play videogames
- 👉🏻 In linux, permissions are always **indirect**
- to get a permission in linux,
- you need to get **added** to the group of ppl who already have the permission
- need to ask `sudo` to help you get added

- `sudo adduser shpl vboxsf`
- `vboxsf`: group of users who can already use shared folders
- if adding your user to `vboxsf` does not work,
- it is bc you failed to install `GA`

**(12) restart/reboot the system**

- `sudo reboot`

**(13) test 2-2: check if shared folders work**

[![2ga12.png](https://i.postimg.cc/DwzWVD1y/2ga12.png)](https://postimg.cc/bsKYkm6K)

- if I was in 1️⃣ graphics mode, and graphics worked
- I can check it by clicking on the `files icon` in the left bar
- shared folder starts with `sf`

- if you are in 2️⃣ commands mode,
- enter `cd /media`
- and check if your shared folder is there

- then list the content of the directory `ls`
- check if your shared folder is there
- and enter it `cd sh_G_DRIVE`
- and list the content using `ls`

[![Screenshot-2026-03-02-at-16-42-56.png](https://i.postimg.cc/d3sXHqdj/Screenshot-2026-03-02-at-16-42-56.png)](https://postimg.cc/5YrnjWsX)

(16) Once everything works, turn off the machine

- we want to take a shapshot
- switch the machine off
- for switching off, now that you have the OS,
- use the switch off button!

[![2ga10.png](https://i.postimg.cc/d3MdwBw4/2ga10.png)](https://postimg.cc/ygPWT0JZ)

[![2ga13.png](https://i.postimg.cc/NG7LKY4G/2ga13.png)](https://postimg.cc/Yj0tP5ZT)

(15) Once everything works, take a shapshot

[![2ga14.png](https://i.postimg.cc/NMvf0P2c/2ga14.png)](https://postimg.cc/wtFdf2kf)

- make sure the machine is off
- change the name of shapshot
- `Ubuntu Fresh install with GA`

//2ga 14

(16) Deploy the VM to another host

- deploy the VM
- do not use `.ova`
- sohee: copy the VM folder to a USB to `E:/`
- sohee: create an access to that USB
- cesar: an create the access to the USB in `C:/`
- cesar: `Macina > nueva > `
  - name: same as sohee
  - folder: and create `VBox folder` inside `C:/`
  - hardware: corresponding to new host, cesar's computer
  - vdi: do not create, use the existing one
  - and navigate to sohee's USB, `E:/`

[![Screenshot-2026-03-02-at-17-03-45.png](https://i.postimg.cc/kgyBtss4/Screenshot-2026-03-02-at-17-03-45.png)](https://postimg.cc/fVJwGx6n)
