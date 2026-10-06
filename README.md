# Pokytos

**Pokytos** Yocto Distribution manifest repository

![pokytos](./Documentation/res/pokytos.png)

### Quick reference
**Cloning the project:**
```Bash
$ mkdir -p ~/repos/pokytos
$ cd ~/repos/pokytos
$
$ repo init -b scarthgap -m default.xml -u https://github.com/filhoDaMain/pokytos.git
$ repo sync
```
<br/>

**Building an image:**
> [!TIP]
> I recommend using a Docker image for this. <br/>
> Check my custom [pokytos-builder](https://github.com/filhoDaMain/pokytos-builder) set up for Yocto builds.

```Bash
$ source init
$ bitbake pokytos-console-image
```
<br/>

**Running an image on QEMU:**
```Bash
$ runqemu nographic slirp
```
<br/>

---
<br/>

# About Pokytos
**Pokytos** is a small Yocto "platform" that I started developing to store my customizations to build a Linux image suitable for Kernel hacking, learning and debugging. It is pretty much a work in progress Yocto platform.
</br>

The following devices are tested:

 
| MACHINE        | Device                       | Kernel                       |
| -------------- | ---------------------------- | ---------------------------- |
| raspi3ap       | Raspberry Pi 3 Model A Plus  | linux-stable (6.12 upstream) |
| opizero3       | Orange Pi Zero 3             | linux-stable (6.12 upstream) |
| qemu-raspi3ap  | QEMU virt platform           | linux-stable (6.12 upstream) |
| qemu-opizero3  | QEMU virt platform           | linux-stable (6.12 upstream) |
</br>

# How-tos
Have a look in the [Pokytos Reference Manual](./Documentation/index.md) I'm working on.
