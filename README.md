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
**Pokytos** is a small Yocto distribution that I created to store my changes to **Poky** in order to build an image suitable for **embedded Linux kernel development / debugging**.

Currently I've been testing this distro in QEMU and raspberrypi3.

# How-tos
A comprehensive [Wiki](https://github.com/filhoDaMain/pokytos/wiki) is currently in progress.
