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