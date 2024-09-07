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