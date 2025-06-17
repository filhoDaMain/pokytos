# Pokytos

**Pokytos** Yocto Distribution manifest repository

### Quick reference
**Cloning the project:**
```Bash
$ repo init -b nanbield -m default.xml -u https://github.com/filhoDaMain/pokytos.git
$ repo sync
```
<br/>

**Building an image:**
> [!TIP]
> I recommend using a Docker image for this. <br/>
> Check my custom [pokytos-builder](https://github.com/filhoDaMain/pokytos-builder) set up for Yocto builds.

```Bash
$ cd pokytos
$ source pokytos-env
$ bitbake pokytos-console-image
```
<br/>

**Running an image on QEMU:**
```Bash
$ runqemu pokytos-console-image nographic slirp
```
<br/>

---
<br/>

# About Pokytos
**Pokytos** is a small Yocto distribution that I started developing to store my customizations to build a Linux image suitable for Kernel hacking, learning and debugging.

Currently I've been testing this distro in QEMU and raspberrypi3.

# How-tos
Have a look in the current [Pokytos Reference Manual](./Documentation/README.md).
