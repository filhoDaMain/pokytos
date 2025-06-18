# Image Build Process

## Index
1. [Target selection](#target-selection)
2. [Available Images](#available-images)
3. [Image Build](#image-build)
4. [Try built image](#try-built-image)
    1. [Real Hardware - Flash SD Card](#real-hardware---flash-sd-card)
    2. [Emulated Target](#emulated-target)

## Target selection

Set **MACHINE** variable to one of the [supported devices](./03_supported_devices.md#list-of-tested-devices).

Example (build/conf/local.conf):
```Bash
MACHINE = raspberrypi3
```
</br>

## Available Images

Build an image, by "bitbaking" the respective Image recipe.


| Image (recipe)   | Notes                                                                        |
| ------------------------ | ---------------------------------------------------------------------------- |
| [pokytos-console-image](https://github.com/filhoDaMain/meta-pokytos/blob/nanbield/recipes-core/images/pokytos-console-image.bb)    | A Linux image with basic functionality to boot into userspace. Console only. |

</br>

## Image Build
Example:
```Bash
# From ~/repos/pokytos-yocto (or after launching pokytos-builder)
$ cd pokytos
$ source pokytos-env
$ bitbake pokytos-console-image
```
</br>

## Try built image

### Real Hardware - Flash SD Card

After bitbaking an image, the output is collected in `pokytos-yocto/pokytos/build/tmp/deploy/images/${MACHINE}/`

NOTE: The SD Card image has **.wic** suffix

**Example:** Flash **pokytos-console-image** built for raspberrypi3:

1. Plug the SD Card into the SD Card Reader
    ```Bash
    # Find which /dev/ device is the SD Card (/dev/sda or /dev/sdb or ...)
    $ lsblk
    ```
</br>

2. Write the .wic image into the SD Card
    ```Bash
    # Example - SD Card is /dev/sda and image was built for raspberrypi3
    $ cd ~/repos/pokytos-yocto/pokytos/build/tmp/deploy/images/raspberrypi3
    $ sudo dd if=pokytos-console-image-raspberrypi3.rootfs.wic of=/dev/sda status=progress
    ```
</br>

3. Plug the SD Card into the target's SD Card Slot and power the device on


### Emulated Target

If **MACHINE** was set to one of the available [emulated devices](./03_supported_devices.md#list-of-tested-devices), to test the the image run:

```Bash
$ runqemu <MACHINE> nographic slirp
```

To exit the emulated device shell: `(Ctrl + A) then X`

![runqemu](../res/runqemu.gif)