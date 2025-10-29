# Kernel Drivers Development
This page describes how to cross develop **out-of-tree** modules for the Linux Kernel using the **Pokytos SDK**.

## Prepare the SDK for out-of-tree module build
### Generate and install an SDK
This is common to any SDK generation and installation.

If you haven't generated and installed the Pokytos SDK yet, see [here](./06_sdk_cross_development.md#quick-reference) how to do it.

### Prepare kernel sources
This step is required to develop out-of-tree kernel modules only.

1. Install the following dependencies
```text
gcc
flex
bison
```

2. Copy the kernel sources from SDK installation to a **directory without root permissions**
```bash
# Eg, copy to ~/sdks/pokytos-rpi3/kernel/:
$ cp -r /opt/pokytos/1.0.0/sysroots/cortexa7t2hf-neon-vfpv4-poky-linux-gnueabi/usr/src/kernel/ ~/sdks/pokytos-rpi3/
```

3. Prepare kernel sources
```bash
# Source SDK env (if you haven't yet in current shell)
# Eg:
$ source /opt/pokytos/1.0.0/environment-setup-cortexa7t2hf-neon-vfpv4-poky-linux-gnueabi

# Go to the directory where you copied SDK's /usr/src/kernel/ into
# Eg:
$ cd ~/sdks/pokytos-rpi3/kernel

# Run
$ make modules_prepare
```

### Cross compile kernel module
1. Source SDK env (if you haven't yet)
```bash
# Eg:
$ source /opt/pokytos/1.0.0/environment-setup-cortexa7t2hf-neon-vfpv4-poky-linux-gnueabi
```

2. Set `KERNEL_SRC` variable to point to kernel sources where `make modules_prepare` was run.
```bash
# Eg.
$ export KERNEL_SRC=~/sdks/pokytos-rpi3/kernel
```

3. *Make* the driver
```bash
$ make
```

As an example, see how [dipslay7](https://github.com/filhoDaMain/display7/tree/main) driver can be compiled in the same way.


## Kernel and drivers debugging
**KGDB** is the *de facto* Linux Kernel debugger which allows the usage of **GDB** as a front-end.

You need to compile the kernel with certain debugging facilities enabled!

### Build with KGDB support
[Offical Guide!](https://docs.kernel.org/process/debugging/kgdb.html)

To simplify, **pokytos-console-image-developer** already enables the necessary kernel features to allow KGDB debugging. Just build the [developer image](./05_multiconfig_builds.md#quick-reference) to pull the correct debug kernel configuration ([example](https://github.com/filhoDaMain/meta-pokytos-bsp/blob/scarthgap/recipes-kernel/linux/files/rpi/debug.cfg))

```bash
# Build and Flash a Developer Image
# to use a Kernel suitable for KGDB debugging
$ bitbake mc:developer:pokytos-console-image
```