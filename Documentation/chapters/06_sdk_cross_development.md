# SDK - cross development

One of the benefits of using Yocto is the ability to easily generate an SDK for cross compilation and debugging.

I devided this chapter in two major goals:

1. [Application Development](./061_app_development.md)
2. [Kernel Drivers Development](./062_kernel_drivers_development.md)

## Quick reference

### Generate SDK for base image
It's advisable to use the developer configuration - see [multiconfig builds](./05_multiconfig_builds.md)
```bash
$ bitbake mc:developer:pokytos-console-image -c populate_sdk
```
This will generate an SDK for the corresponding **MACHINE** for which it was built.

### Install the SDK
By default, SDK installer is a shell script found at:
`build/tmp-developer/deploy/sdk/`.

Run the script to install the SDK in your machine.

### Usage - C/C++ cross compilation
To compile an application (C or C++) you need to source the SDK environment file. Then, proceed with the usual *make* target steps.

*Eg.*
```bash
# Source the ENV file to use the $CC cross-compiler for your target
$ source /opt/pokytos/1.0.0/environment-setup-cortexa7t2hf-neon-vfpv4-poky-linux-gnueabi
$ make <target>
```