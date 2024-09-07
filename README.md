# Pokytos

**Pokytos** Yocto Distribution manifest repository

### Quick reference
**Cloning the project:**
```
$ repo init -b nanbield -m default.xml -u https://github.com/filhoDaMain/pokytos.git
$ repo sync
```

**Building an image:**
```
$ cd pokytos
$ source pokytos-env
$ bitbake pokytos-console-image
```

**Running an image on QEMU:**
```
$ runqemu pokytos-console-image nographic slirp
```
---
---

## About Pokytos
Pokytos is a small Yocto distribution that I created to easily store my changes to **Poky** (that I've been kepting arround locally on my PC) in order to build an image **suitable for embedded Linux kernel development/debugging**. Needless to say it's extensivily based on Poky distro :)

My aim was to create a distro which enabled me to easily apply or disable all required Linux configurations to support interactive debugigng with KGDB, for both kernel and loadable modules debugigng.

I'm currently using a raspberrypi3 and QEMU (arm) to test these changes, so, for now, these are the "officialy unoficial" supported platforms.