# Initial Setup

## Index
1. [Cloning all repositories](#cloning-all-repositories)
    1. [Install repo tool](#install-repo-tool)
    2. [Initialize the project repo](#initialize-the-project-repo)
    3. [Sync all repositories](#sync-all-repositories)
2. [Build First Image](#build-first-image)


## Cloning all repositories

**Pokytos** depends on multiple [Yocto Meta Layers](https://docs.yoctoproject.org/current/overview-manual/yp-intro.html#the-yocto-project-layer-model), which are cloned as separate git repositories.

The full list of git repositories is defined in a [*Manifest*](https://github.com/filhoDaMain/pokytos/blob/nanbield/default.xml) file which describes:
- The URL of each git repo to be cloned;
- Which branches or fixed-commit hashes to checkout;
- Where to clone each git repo.

We use these Manifest files with [repo](https://gerrit.googlesource.com/git-repo), a tool developed by Google to manage projects consisting of multiple git repositories.

### Install repo tool
> [!TIP]
> Install the latest python version before proceeding. <br/>

**Download** <br/>
I like to keep the tools I use in a directory `~/tools/`. Be free to download repo to anywhere of your preference.
```Bash
$ mkdir -p ~/tools/repo-tool/

# Download
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/tools/repo-tool/repo

# Make downloaded python script executable
$ chmod a+rx ~/tools/repo-tool/repo
```
<br/>

**Install** <br/>
```Bash
$ sudo cp ~/tools/repo-tool/repo /usr/local/bin/
```
<br/>

**Check Installation Success** <br/>
```Bash
# From any directory, should retrieve the repo tool version
$ repo --version
```
<br/>

Now with **repo** tool installed we can use the [*Manifest*](https://github.com/filhoDaMain/pokytos/blob/nanbield/default.xml) to clone all repositories.

In "**repo world**" this is done in 2 steps:
- **Initialize the repo**
- **Sync'ing all repositories**
<br/>

### Initialize the project repo
This consists in cloning the manifests repository and reading the meta-data from one of the Manifests.

```Bash
# Create a base folder, where everything will be cloned into
$ mkdir -p ~/repos/pokytos-yocto
$ cd ~/repos/pokytos-yocto

# Initialize the repo
# * Manifests repo URL: https://github.com/filhoDaMain/pokytos.git
# * Which branch: nanbield
# * Which Manifest to use: default.xml
$ repo init -b nanbield -m default.xml -u https://github.com/filhoDaMain/pokytos.git
```
This will create directory `~/repos/pokytos-yocto/.repo`, where the manifests repo is cloned and meta-data used by the tool created.
<br/>

### Sync all repositories
This step will clone all repositories described in the Manifest which we used earlier. In our case, it will clone all **Pokytos Yocto Layers**.

```Bash
# From ~/repos/pokytos-yocto
$ repo sync
```

Usually you only **repo init** once and **repo sync** always prior to start developing changes.

This way you work always with the most updated version of the Project.
<br/>


## Build First Image

To test our initial setup we will compile a simple image for an emulated target - **qemuarm** . No extra configuration is needed, as this is the default **target MACHINE**.

> [!TIP]
> I recommend using a Docker image for this. <br/>
> Check my custom [pokytos-builder](https://github.com/filhoDaMain/pokytos-builder) set up for Yocto builds.

```Bash
# From ~/repos/pokytos-yocto (or after launching pokytos-builder)
$ cd pokytos
$ source pokytos-env
$ bitbake pokytos-console-image
```

To test the image run (in the same shell where pokytos-env was sourced)
```Bash
$ runqemu qemuarm nographic slirp
```

To exit the emulated device shell: `(Ctrl + A) then X`