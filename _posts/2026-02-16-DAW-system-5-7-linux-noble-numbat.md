---
title: 5.7 Incidents in installation
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

✔️ **Pin the terminal**
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

✔️ **BASH**

> Bowne Again SHELL

- Bowne: best friend of Linux
- in every linux, the command shell is normally named after a person

✔️ **Prompt**
[![28-prompt.png](https://i.postimg.cc/DwCnXtJq/28-prompt.png)](https://postimg.cc/xXbwrpPC)

- the commands line is called `prompt`

- `technical name` @ `computer name` : `my directory` $

`shpl@shpl-VirtualBox:~$`

- `shpl`: technical name
- `VirtualBox`: computer name
- `~`: my personal folder
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

- ⚠️If you see `#`, logout
