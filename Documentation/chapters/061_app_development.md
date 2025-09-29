# App Development

## Cross compilation
1. Generate and install an SDK - see [here](./06_sdk_cross_development.md#quick-reference).

2. Source the SDK environment
```bash
# Eg.:
$ source /opt/pokytos/1.0.0/environment-setup-cortexa7t2hf-neon-vfpv4-poky-linux-gnueabi

# Check cross-compiler was set
$ echo $CC
```

3. Use Makefile tools as usual or call compiler $CC
```bash
$ make
```

## Remote Debugging

> [!TIP]
> Compile application with -ggdb flag for GDB support

Install `gdbserver` in target image. </br>
**NOTE:** [pokytos-console-image-developer](./05_multiconfig_builds.md#quick-reference) should already include this package by default.

### Terminal UI (cgdb)
Install `cgdb` in Host machine.

Start application (e.g `helloworld`) in target using **gdbserver**
```bash
# Use an available port (e.g. 2001)
$ gdbserver :2001 ./helloworld

# gdbserver will wait for a connection on that port
```

From **Host machine**, connect to target's `IP-address:port` and pass cross-compiled application with **debugging symbols** (*unstripped*) as an argument.
```bash
# From Host Machine...

# Source SDK if not done yet
$ source /opt/pokytos/1.0.0/environment-setup-cortexa7t2hf-neon-vfpv4-poky-linux-gnueabi

# Use SDK's cross-debugger and invoke cross-compiled app
$ arm-poky-linux-gnueabi-gdb helloworld
```

**From GDB interactive shell:**
```bash
# Inside GDB, connect to remote target
# Use IP:port (e.g. host pi and port 2001)
>> target remote pi:2001
```

### VSCode Frontend Configuration

Install [Native Debug](https://marketplace.visualstudio.com/items?itemName=webfreak.debug) extension.

Recommended: install [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) extension.

For a complete setup follow the example from [helloworld_debug](https://github.com/filhoDaMain/helloworld_debug).

Copy the `.vscode` from the Reference App to your application's VSCode Workspace and adapt paths accordingly.
