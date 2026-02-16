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

- 😱 Incident: does not install
- If ubuntu does not install
- disable the `SVGA`
- or disable the `3D`
- in order to weaken the VM

[![Screenshot-2026-02-16-at-17-45-06.png](https://i.postimg.cc/3Jpgqk7v/Screenshot-2026-02-16-at-17-45-06.png)](https://postimg.cc/PPXpprCX)

- Invalid settings: sometimes it is needed

- 😱 Incident: button does not appear
- even if you have `SVGA`,
- the continue button might not appear
- 💊 click on `tab`, then click on `enter key`

- 😱 Incident:
- everything is installed,
- but the next day, the machine does not boot
- ❓ why does this happen? we gave the required minimum RAM
- 💊 give more RAM

- 😱 Incident: mouse disappears
- after when everything is installed, mouse disappears
- ❓ why does this happen? not enough graphic power
- 💊 enable `3D acceleration`, enable `SVGA`
- mouse only work when minimum requirements are satisfied
- so before installing, maybe disable `3D acceleration` and `SVGA`
- then after installing, if mouse is gone, enable `3D acceleration` and `SVGA`

- 💡 Note:
- same `.iso` can behave differently depending on the host

## ✅ Summary

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
