# Supported Devices

You set up the target device by assigning the corresponding value to [MACHINE](https://docs.yoctoproject.org/ref-manual/variables.html#term-MACHINE) variable in `pokytos-yocto/pokytos/build/conf/local.conf`

> [!NOTE]  
> **build/** dir is created after sourcing pokytos-yocto/pokytos/pokytos-env for the first time

Example - set up target device as Raspberry Pi 3 (32-bit)
```Bash
MACHINE = "raspberrypi3"
```

**NOTE:** The default MACHINE variable (qemuarm) comes from `meta-pokytos/conf/templates/default/local.conf.sample`, which you can customize to make it version controlled.

**List of Tested Devices**
 
| MACHINE      | Defined in Layer | Device                                              |
| ------------ | ---------------- | --------------------------------------------------- |
| qemuarm      | meta             | Emulated, ARM 32-bit                                |
| raspberrypi3 | meta-raspberrypi | RPI3 (all versions) in 32-bit mode - SoC: BCM2837B0 |

</br>

Once **MACHINE** variable is set, bitbaking an image like **pokytos-console-image** will produce an image cross-compiled for the corresponding device.

After build, the image and output artifacts are collected in `pokytos-yocto/pokytos/build/tmp/deploy/images/${MACHINE}/`