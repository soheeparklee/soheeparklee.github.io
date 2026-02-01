---
title: 4.4 Virtual Machine Setting
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## 💡 .vbox

- ❓ Where can I see `.vbox` and `.vdi` folders?
- `scaffold` > `right click` > `show in explorer`

- `.vdi 2 megas` is always the min size of a dynamic vdi
- when we create a VM, the vbox only contains RAM, cores, BIOS
- The `.iso` file is an installer, it could be an OS, app to run

## 💡 Adding extra settings to the VM

- Scaffold > Configuration ➡️ Window that gives lot of info about extra things in a
  VM:

  - Every window here is specified with the option of menu a dot and the name of label `Menu.label`
  - According to versions and characteristics of hardware for each one the label’s name are different.

- There are two ways to see this
- 1️⃣ basic
- 2️⃣ expert: for technicians

## 📌 General label

### ✅ general.basic

[![general-basico.png](https://i.postimg.cc/jdWYGpWV/general-basico.png)](https://postimg.cc/zV1QhPSp)

✔️ **Name**

- change name of VM for the last time
- ⚠️ chaning VM name later will unlink files of the VM once started!

✔️ **Fields like type, subtype, version**

- type, subtype, version can be changed here if they are not filled
- ⚠️ also last chance
- some `.iso` files do not fill these fields automatically
- If we do not fill it, the VM will have mistakes when we start
- bc the specification of the `iso` files do not match

```
👀 An iso file with type windows, subtype 10
without the field version filled,
the system will filled this by default with the host arch settings.
```

### ✅ general.avanzado

[![general-avanzado.png](https://i.postimg.cc/rmKLM3hP/general-avanzado.png)](https://postimg.cc/VrQhFGPq)

✔️ **Spapshot folder, carpeta de instaneas**

- folder where the recovery points are saved
- recovery point: when we want to go back
- ⚠️ If we change this manually the snapshots could get unlinked, don’t do it.
- This is a subfolder in the VM folder

✔️ **Clipboard, corta papeles**

- portion of the RAM for copying and pasting data

✔️ **Shared functionally**

- for copy and paste data from host to guest
- importatnt for sharing information trough machines
- recommended to set it in bidireccional (copy & paste)

✔️ **Drag ‘n drop**

- Is not copying, is moving and pasting, must set to bidireccional
- This two functionallities are not activated until you add an extra package
  for security reasons
- GUEST ADDITIONS

```
⭐️ Guest Additions
GUEST ADDITIONS complementos del invitado
- installed manually,
- needed for bidireccionality
- it cannot be installed until there is at least one OS in my VM
- For each OS is a different guest additions package

- In VM guests changes every time we add a VM
- In the VM in the aula the guest is GParted
- as GParted is not an OS we don’t installed guest additions (they are
only for OS)
- after we install Windows it will be my host
- then Lin on top of Windows and it will be the host.
```

### ✅ general.description

[![general-description.png](https://i.postimg.cc/QCB22z8t/general-description.png)](https://postimg.cc/8fSXWtrQ)

- Mandatory when we deploy (desplegar) our VM
- high level description of a virtual machine
- it says thoroughly what the vm says

```
VM over dynamic 100GB virtual disk created internally in host for dual
booting Linux and Windows on a hardware limited computer adding
tunnelling, distrohopping and making sure that both OS systems boot
independently no matter future changes.
```

### ✅ general.disk encryption

[![general-cifrado-De-Disco.png](https://i.postimg.cc/3xQsq9P3/general-cifrado-De-Disco.png)](https://postimg.cc/0bZXMGk4)

- setting for transparent encryption
- encrypting the `.vdi` with a key in my unit 0 of the real disk
- or in the TPM(`.vdi` does not have a unit 0)
- `.vdi` does not have specific booting if the real disk boots

- it should be activated when we have private information(👀 passwords)
- 👀 the HR of a company should be encrypted or ethic hackers

- Do not enable unless is needed, encryption overloads the VM
- Remember that hashing which is the same as encryption, modifyes totally the data even with a little change

```
⭐️ ETHICAL HAKING
Hacking with a good purpose.
Whe we design hacking,
the VM should be ecrypted to avoid infections into the real machines
```

## 💡 Enable hardware watch(clock)

- Enable hardware watch(clock)
- you are getting the real machine data and time
- and you are giving that to the VM
- purpose: both VM and RM are syncrhonized
- when would you not want to synchornize the VM with the RM
- when you want to make a worm and play around

## 📌 System label

### ✅ System.motherboard

[![system-placabase.png](https://i.postimg.cc/jqQ35K9r/system-placabase.png)](https://postimg.cc/14Xr7xsW)

✔️ **Memoria base**

- change the size of RAM given to the VM

```
👀 If we have a windows 10 32b
 .iso and the RAM is 4098MB (4096MB = 4GB),
this system will not boot wahsh it down to 4000 not to the limit.
sometimes more is less
```

✔️ **Boot order**

- same as boot sequence (which device will boot: HD or USB bootable)
- remember this is not the same as bootstrap loader(which OS boots= GRUB)

- there are four options(although first two are mainly used)
- 1️⃣ Optical CD: `iso` this is first, this means: boot with `.iso` and forget what is in the harddisk
- 2️⃣ Hard disk: `.vdi` this is first, this means: boot with harddisk and forget what it is in the `iso`
- 3️⃣ untick diskett is not used
- correct order and options ticked

- when the `.vdi` is created, it is empty
- in Virtualization, if the `.vdi` is first, the machine will not boot
- this is an order that excludes, will show the error `No Bootable media found`

```
👀 If we have windows and we want to install Linux,
which option should I use for the boot order,
and what iso should I exclude?

- Optical = iso
- Harddisk
- if we do it backwards, linux will never be read
```

- 4️⃣ network installation: sometimes network installation is also possible

✔️ **Chipset**

- Dual chips: northbridge and southbridge
- NB helps with important things
- 🛠️ RAM, Graphics FSB

- SB helps with not so important things big chip
- 🛠️ USBs, microphones, speakers(external connection)

- These days, the northbridge goes inside the CPU and lost functionalities
- the SB now called `PCH` does more things getting hotter
- Here we have to decide if we want traditional system or modern PCH, remember it is not what I have, it is what I want.

[![Screenshot-2026-02-01-at-00-58-56.png](https://i.postimg.cc/bNnJbCxw/Screenshot-2026-02-01-at-00-58-56.png)](https://postimg.cc/bszpfRV7)

- `PIIX3`: NB and SB called like this due to the first computer that has this structure
- 🛠️ choose PIIX3 when the vm doesn’t need much power in graphics
- 🛠️ simple OS
- `ICH9`: PCH modern structure
- 🛠️ strong OS

```
👀
GParted. iso → PIIX3
Mac OS→ ICH9
iOS → ICH9
Win32b → PIIX3
Win ≥ Vista 64b → ICH9
Linux ? should be flexible
```

- ⚠️ Sometimes chipset is not available
- because of backwards compatibility,
- which means if a `host has ICH9` and the `VM will use ICH9` it will work with iso files, this is valid but not perfect.

- Normally using `ICH9` needs more energy

- TPM means if you want to simulate TPM for Windows 11 OS option v2

- Some selections are flexible and others are strict,
- Whenever you tick something that is strict
- it will appear an option `Invalid settings detected`
- example disk encryption is strict only tick when needed
- Selecting the TPM when we don’t need it means overloading the CPU in my computer

[![Screenshot-2026-02-01-at-01-04-34.png](https://i.postimg.cc/65V8gb8J/Screenshot-2026-02-01-at-01-04-34.png)](https://postimg.cc/qzRBCLcj)

✔️ **Pointing device mouse**

[![Screenshot-2026-02-01-at-01-07-35.png](https://i.postimg.cc/tR3R4ZpX/Screenshot-2026-02-01-at-01-07-35.png)](https://postimg.cc/5jtWPtXG)

- `PS2` is you want the vm mouse to behave as the standard mouse
- blinks at low speed

- `Tablet USB`: means new USB
- high speed
- To use the tablet usb, the USB should be readable for the vm so it will only be valid
  when we have the extension pack
- Many companies reject the extension pack
- they don’t want you to do the things your way.
- in this case, if we don’t have the extension pack, we have to use PS2 option
- conclusion: choose the most modern possible pointing device, making sure that
  is valid add ss of extension pack and tablet

✔️ **I/O APIC**

> Input/Output Advanced Programable Interrupt Controller

[![Screenshot-2026-01-28-at-15-58-17.png](https://i.postimg.cc/dQWCksg3/Screenshot-2026-01-28-at-15-58-17.png)](https://postimg.cc/hhdvNBDR)

- Peripherals = input output
- Interruption = error
- 💡 8 shape: If there is an interruption, we go to the verctors table, it sends us down to the service routine, solved by execution of a command and I come back to where I was before

- If we activate this option we are asking for help to the peripherals
- we should do it when :
- 1️⃣ More than 1 virtual core: mandatory, must tick on `I/O APIC`
- bc you have two bosses(cores) interrupting
- if we untick the `invalid settings detected` will appear
- 2️⃣ app or OS has 64b optional

- after you start the OS, you will not be able to tick/untick the `I/O APIC`
- ⚠️ so becareful

```
Virtual Box 7 chooses I/O APIC auttomatically, v5 doesn’t.

❓ Why companies with v5 stayed this way?
- Upgrading means leaving traces from older versions
- in companies these traces must be cleaned computer by computer and they can make the scaffolds dissapear
```

✔️ **EFI**

- ⚠️ last opportunity to change this
- **OS specials**: this is telling you this is needed in a `OS Win ≥ grater
Vista 64Gb `
- If we tick this we have the possibility of activating the secure boot
- Linux does not accept secure boot

### ✅ system.procesador

[![system-procesador.png](https://i.postimg.cc/xTs2XL70/system-procesador.png)](https://postimg.cc/zVRMMH8M)

✔️ **Cores**

- ⚠️ last chance to change core number

✔️ **Execution Cap, Limite de ejecucion**

- 1️⃣ If the execution is **100%**, there is no limit on the VM
- obviously, there will always be RAM, cores limit
- but other than those, there is no other limit

- 2️⃣ If the execution is **lower than 100%**, weakens the VM
- you do it to weaken the VM
- and give the power to the RM
- do it when the VM is so demanding, it is being too strong
- the VM is eating too much of your RM
- and the RM will run better
- Setting the Exec limit down means weakening the VM and giving better performance or extra power to the real machine.

- 3️⃣ If the execution is **0%**
- you are making the VM stop/freeze
- which means 🟰 stopping
- it does not mean shutting down the VM ❌
- 🛠️ to protect your VM from VM malware
- 💡 **VM malware**: a VM that enters your computer without your permission, and starts running
- if you have a VM malware, you set the limitation cap of all the VMs to 0%
- then, go one by one and for only the VMs you know and are official, set it back to 100%

✔️ **PAE/NX**

[![system-procesador.png](https://i.postimg.cc/xTs2XL70/system-procesador.png)](https://postimg.cc/zVRMMH8M)

- 1️⃣ **PAE**
- P: Physial
- A: Address ➡️ RAM
- E: extension
- ➡️ RAM Extension
- ➡️ SWAP
- use harddisk help

```
if RAM of the VM < 4GB then SWAP = RAM*2
if RAM of the VM = 4GB then SWAP = RAM
if RAM of the VM > 4GB then SWAP = RAM/2
```

- 💡 Note: Tick PAE, if RAM <= 4 GB
- Do not tick PAE only if RAM > 4GB
- Also try to save some SWAP, save some harddisk, if you do not need

- ❓ **Why not tick PAE in every condition?**
- bc PAE is taking space from your SWAP, your HD

- 2️⃣ **NX**: Non execute
- Flag that you exable for suspicious processes
- 👀 suspicious processes: process that tries to enter the OS in RAM
- then you enable NX flag for that processes
- if the antivirus sees a process with the NX flag,
- antivirus will capture it and **swap out three generations** from the process from the RAM
- in order to see the generations of the process,
- we need to do a query of the **processes table** in **OS in RAM**

- ❓ **Why is PAE joined to NX?**

- bc I need to capture the suspicious process and make queries
- and these queries are overusing the RAM
- and you are increasing the waiting time for the good processes
- so you use the help of SWAP
- so that standard processes do not have to wait so much

- 💡 Note: not all process needs protection in a computer
- 👀 pings can fail, but as it is repeated, it can fail as long as it is repeated

### ✅ system.aceleration

[![Screenshot-2026-01-28-at-15-54-54.png](https://i.postimg.cc/TPy7SNmJ/Screenshot-2026-01-28-at-15-54-54.png)](https://postimg.cc/hJB1Qr2X)

- the RAM always gives more priority to the RM processes
- VM processes have worse priority
- if you activate accerleration,
- you balance all processes of both RM and VM

- tick means: balancing

## 📌 Pantalla

### ✅ Pantalla.pantalla

[![Screenshot-2026-01-28-at-16-02-31.png](https://i.postimg.cc/43LKKwF6/Screenshot-2026-01-28-at-16-02-31.png)](https://postimg.cc/NyXGS8tF)

✔️ **memoria de video**

- RAM of your graphics card
- modern graphics card have their own RAM for speed purposes
- memoria de video(Grpahic card) does DMA, they have their own RAM ⭕️
- it does not do PIO anymore ❌

```
PIO: doing the 8 in the RAM
DMA: Direct Memory Access, having your own RAM
```

- If I have a graphics card in my RM that has a RAM,
- how much of the total RAM of grphics card should I give to the RAM?
- **maximum half** of the RAM of grphics card to the VM

✔️ **numero de monitores**

- several screens in your VM
- leave it as default
- when we tick this option, we need to choose how much percentage we want for scallatoin through monitors

✔️ **Factor de escalado**

- how to split VM to several monitos
- scale: give 40% of VM to screen 1, give 60% of VM to screen 2...

✔️ **Graphic controller**

- controlador grafico
- **resolution** you are giving to the screen of the VM

- 💡 **Two types of resolution**
- 1️⃣ `VGA` : low resolution, width and height lower than 800px
- 2️⃣ `Super VGA`: high resolution, width and height more than 1000px
- we need `SVGA` for VM when the VM needs high resolution

- 🛠️ high resolution: when `GUI` is important
- we always need to check the specs of the `iso`
- if we have a VM buttons that disappears,
- it is bc you should have given `SVGA`, but you did NOT! 😱

- ❓ Why not give `SVGA` always?
- do not give a `SVGA` to an application that wants `VGA`
- it can make an `.iso` not to work, bc you are demanding too much resolution

✔️ **Two types of SVGA**

[![Screenshot-2026-01-28-at-16-16-15.png](https://i.postimg.cc/wTw34w99/Screenshot-2026-01-28-at-16-16-15.png)](https://postimg.cc/KRgZRrKW)

- 1️⃣ `VMSVGA`: the perfect controller for that specific `.iso`
- 2️⃣ `VBoxSVGA`: standard controller offered by virtual box, with minimum requirements

- if the `.iso` needs `VMSVGA`, do not give `VBoxSVGA`
- some `.iso` do not have `VMSVGA`, so you need to choose `VBoxSVGA`

### ✅ Acceleration 3D

- tick only if the specifications of the `.iso` demands on its specs
- 🛠️ for videos, movements
- do not tick by default

## ✅

## ✅

#### 1️⃣

#### 2️⃣

#### 3️⃣

#### 4️⃣

- 1️⃣
- 2️⃣
- 3️⃣
- 4️⃣
  👍🏻
  👎🏻

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓
👉🏻
```
