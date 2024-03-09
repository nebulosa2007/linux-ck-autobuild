# linux-ck-autobuild
## About
> Linux-ck is a package that allows users to run a kernel and headers setup patched with Con Kolivas' -ck patchset, including hrtimer patches and the 1000 Hz tick rate and others cpu optimizations correspond to -march= settings: generic-v2,3,4 or specific subarch. Also you can choose Clang compiler rather that GCC.

https://wiki.archlinux.org/title/Unofficial_user_repositories/Repo-ck

## Features

* Automatically builds desired architectures
* Daemon which monitors for new releases and automatically starts the build script
* Compatible with modprobe-db
* Custom commands that can be run after the build script
* Automatically checks the ck repo for pre-built kernels
* Option to add build kernels to your local repo with archive of obsolete packages
* Frofiles support
* Ability to build needed commit (version) of linux-ck PKGBUILD (e.g. for compile old versions)
* Automatically adds and applies *.patch files before the build process.

## Installing

This package can be installed from the [![linux-ck-autobuild](https://repology.org/badge/version-for-repo/aur/linux-ck-autobuild.svg?header=AUR:%20linux-ck-autobuild)](https://aur.archlinux.org/packages/linux-ck-autobuild)


## Usage
First you'll need to setup the configuration file, simply by running ``linux-ck-autobuild`` from a command line. The script will notify you about configuration missing and will copy the default config to your home folder. Directions are given in the configuration file.

The minimum options you'll have to modify will be the SUBARCH (the micro architectures you want to build) and probably the BUILD_DIR, which sets the location where the builds take place (don't worry, you don't have to download anything yourself). SUBARCH also can be modify by ``linux-ck-autobuild -a``

Profiles:
Use ``linux-ck-autobuild -n mypc1`` to add a new profile, then uncomment/edit desired parameters which should be differ from default profile. After editing you should write name of profile on desired order of compiling - ``linux-ck-autobuild -c``, then edit: ``PROFILES=( mypc1 linux-ck-autobuild )``

The configuration can be accessed at any time by running ``linux-ck-autobuild -c [profile_name]`` from a command line.

If you want to fully automate the build script, enable the daemon by running:
```
linux-ck-autobuild -c # Configure first required! Set EDITOR and other parameters as desired
linux-ck-autobuild    # Check work of script and only then:
sudo systemctl enable --now linux-ck-autobuild@$USER.timer
```
## Minimum requirements for building archlinux kernel (-ck)
* CPU (x86_64): any. More cores and MHz - less compile time.
* RAM+SWAP: peak to 8Gb* for btf.o compile (since [5.7.1.arch1-1](https://gitlab.archlinux.org/archlinux/packaging/packages/linux/-/commit/2db27e8ef8a6ca7c801082dcad3ad3ddf42c424d))
* Disk space: 25Gb*

  *Or less, if you use [modprobed-db](https://wiki.archlinux.org/title/Modprobed-db), depends how many modules you want to compile
