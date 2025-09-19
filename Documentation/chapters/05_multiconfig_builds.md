# Multiconfig builds

Multiconfigs allow to build the same image with an alternate configuration. This is specially interesting during **development** when some debugging utilities make sense to be included but not during production.

Pokytos meta layer includes a [**developer**](https://github.com/filhoDaMain/meta-pokytos/blob/nanbield/conf/multiconfig/developer.conf) alternate configuration.

## Quick reference
Production / Release image:
```bash
$ bitbake pokytos-console-image
```

Developer image:
```bash
$ bitbake mc:developer:pokytos-console-image
```

## How it works

Sourcing the [**pokytos/pokytos-env**](https://github.com/filhoDaMain/meta-pokytos/blob/nanbield/scripts/pokytos-bitbake-env) applies the base configuration from [local.conf.sample](https://github.com/filhoDaMain/meta-pokytos/blob/nanbield/conf/templates/default/local.conf.sample), by creating a **build/conf/local.conf** with same contents.

[**developer.conf**](https://github.com/filhoDaMain/meta-pokytos/blob/nanbield/conf/multiconfig/developer.conf) is a multiconfig file which adds '**developer**' as a MACHINEOVERRIDES
```bash
MACHINEOVERRIDES:append = ":developer"
```

Recipes which need to differente between release and developer builds can use the **developer** override.

*Eg.*, the [**linux-stable**](https://github.com/filhoDaMain/meta-pokytos-bsp/blob/nanbield/recipes-kernel/linux/linux-stable/include/raspberrypi3.inc) recipe adds extra debugging kernel configurations only when this recipe is built for a **developer** image by <ins>making use the override syntax</ins> as follows:
```bash
SRC_URI:append:developer = "\
    file://debug.cfg \
"
```

You can customize your recipes from any layer in the same way.

## Build
Source the base environment as usual.
```bash
$ source pokytos-env
```

To include an alternate config during a build, bitbake syntax is as follows:
```bash
$ bitbake mc:<config>:<target>
```

Bitbake will look for and apply the configurations from `meta-pokytos/conf/multiconfig/<config>.conf`on top of the base configuration sourced earlier.

*Eg.*, to build a **pokytos-console-image** in which **developer** overrides are included do:
```bash
$ bitbake mc:developer:pokytos-console-image
```

Build Artifacts which are different from base configuration (including the final developer image) are found in a separate **TMP** directory:
`build/tmp-developer/`
