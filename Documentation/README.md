# Pokytos Reference Manual

# Index
1. [Initial Setup](#initial-setup)
2. [Build and run an image](./chapters/02_build.md)

</br>

# Initial Setup

## Repo tool
Install the latest version of [repo](https://gerrit.googlesource.com/git-repo) tool.

You can either do it via your distro's package manager or as I prefer to do it by downloading and installing its sources:
```bash
# Download to 'downloads' directory
$ mkdir -p ~/downloads
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/downloads/repo

# Set executable permissions
$ chmod a+rx ~/downloads/repo

# Install
$ sudo mv ~/downloads/repo /usr/local/bin/repo
```

## Clone all project's repositories
We'll clone the project into `~/repos/pokytos/` directory.

```bash
$ mkdir -p ~/repos/pokytos
$ cd ~/repos/pokytos
$
$ repo init -b scarthgap -m default.xml -u https://github.com/filhoDaMain/pokytos.git
$ repo sync
```
</br>

After `repo sync` your **pokytos** directory should look like this:
```text
.repo/
init -> layers/meta-pokytos/scripts/pokytos-bitbake-env
layers/
```
</br>

## Create directories for `sstate-cache` and `bitbake downloads`
It is highly advisable to keep the **shared state cache** and **bitbake downloads** directories outside of the project so that they can be re-used by other Yocto projects we may have in our build PC.

We'll save the [sstate-cache](https://docs.yoctoproject.org/scarthgap/ref-manual/variables.html#term-SSTATE_DIR) and [downloads](https://docs.yoctoproject.org/scarthgap/ref-manual/variables.html#term-DL_DIR) into `~/data/bitbake.sstate` and `~/data/bitbake.downloads` respectively.

```bash
$ mkdir -p ~/data/bitbake.sstate
$ mkdir -p ~/data/bitbake.downloads
```
</br>

## Install Docker Image for Yocto builds
**Using Docker is not a requirement to build Yocto**, although I think it helps to keep the build environment separate from the host OS configurations.

If you prefer to not use Docker be sure to manage the [Yocto dependencies](https://docs.yoctoproject.org/scarthgap/ref-manual/system-requirements.html#required-packages-for-the-build-host) yourself.


In this section I'll guide you on how to use the Docker Image I created - [pokytos-builder](https://github.com/filhoDaMain/pokytos-builder).
</br>
Once installed, you won't need to manage any Yocto dependency at all.

### Build pokytos-builder Docker Image
```bash
# Clone pokytos-builder repository into anywhere of your preference
$ mkdir -p ~/downloads
$ cd downloads
$
$ git clone https://github.com/filhoDaMain/pokytos-builder.git
$ cd pokytos-builder
$ ./build.sh
```

### Install
**If you followed the suggestions of this Wiki** and cloned **Pokytos** project into `~/repo/pokytos` and created the empty directories `~/data/bitbake.sstate` and `~/data/bitbake.downloads`, **there's nothing left to do besides running**:
```bash
$ sudo ./install.sh
```

#### Observations:
- **If you cloned pokytos into a different directory**, be sure to specify that directory as the first path in [MOUNT](https://github.com/filhoDaMain/pokytos-builder/blob/main/MOUNT) file before running `sudo ./install.sh`
- **If you intent to use different paths for the sstate-cache and bitbake downloads**, be sure to include those paths in [MOUNT](https://github.com/filhoDaMain/pokytos-builder/blob/main/MOUNT) file before running `sudo ./install.sh`
</br>

### Launch pokytos-builder container
After installation you should be able to run from anywhere:
```bash
$ pokytos-builder.sh
```

Inside the Docker container:
```bash
$ pwd
/home/<your-user>/repos/pokytos

$ ls -lh
init -> layers/meta-pokytos/scripts/pokytos-bitbake-env
layers

$ ls -lh ${HOME}/data
bitbake.downloads
bitbake.sstate
```

If **pokytos**, **sstate-cache** and **bitbake downloads** directories were correctly mounted by `pokytos-builder.sh`, you are set to [Build first image](./chapters/02_build.md#build-and-run-an-image)
