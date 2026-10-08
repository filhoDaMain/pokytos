Return to [index](../README.md)

# Build and run an image

<ins>**NOTE**:</ins> From this point onwards it is assumed <ins>you are working in an environment compatible with Yocto builds</ins>, whether that means you've setup your host PC accordingly or you are <ins>**working inside pokytos-builder**</ins> container as I have recommended [before](../index.md#install-docker-image-for-yocto-builds).

---
</br>

## Build

### Source environment setup script

From pokytos rootdir
```bash
$ source init
```

The **init** script "activates" `bitbake` and enables all layers from pokytos. The `build` directory is created first time the script is sourced.

> [!NOTE]
> **First time sourcing init?**
>
> * Now it's time to **add your own configurations** to `conf/site.conf`.
> * This file, inside `build` directory, is where users can add configurations which are particular to their build machine.
> * For example, you can setup the sstate-cache and bitbake downloads directory paths here.
> *
>     ```bash
>     /build$ vim conf/site.conf
>     ```
>     ```bash
>     # E.g. build an SDK compatible with an Apple Silicon machine arch
>     SDKMACHINE ?= "aarch64"
>     
>     # Downloads and sstate-cache local dirs
>     DL_DIR ?= "${HOME}/data/bitbake.downloads"
>     SSTATE_DIR ?= "${HOME}/data/bitbake.sstate"
>     ```

</br>

### Select target device

Assign to `MACHINE` variable from `conf/local.conf` the corresponding target device value.

</br>

### Build image
```bash
/build$ bitbake <image>
```

|               Image                 |              NOTES               |
|-------------------------------------|----------------------------------|
|  pokytos-console-image              | A CLI-only Reference Image       |
|  mc:developer:pokytos-console-image | Developer version of same image  |

</br>

## Run image