# linux-ck-autobuild service

## About 
> Linux-ck is a package that allows users to run a kernel and headers setup patched with Con Kolivas' -ck patchset, including hrtimer patches and the 1000 Hz tick rate and others cpu optimizations correspond to -march= settings: generic-v2,3,4 or specific subarch. Also you can choose Clang compiler rather that GCC.

https://wiki.archlinux.org/title/Unofficial_user_repositories/Repo-ck

## Features

* Automatically builds desired architectures
* Daemon which monitors for new releases and automatically starts the build script
* Compatible with modprobe-db
* Custom commands that can be run after the build script
* Automatically checks the ck repo for pre-built kernels
* Option to add build kernels to your local repo

## Installing

This package can be installed from the AUR:
https://aur.archlinux.org/packages/linux-ck-autobuild (out-of-date)

## Usage
First you'll need to setup the configuration file, simply by running ``linux-ck-autobuild`` from a command line. The script will notify you about configuration missing and will copy the default config to your home folder. Directions are given in the configuration file.

The minimum options you'll have to modify will be the SUBARCH (the micro architectures you want to build) and probably the BUILD_DIR, which sets the location where the builds take place (don't worry, you don't have to download anything yourself). SUBARCH also can be modify by ``linux-ck-autobuild -a``

If you want to fully automate the build script you can enable the daemon by running:

``sudo systemctl enable linux-ck-autobuild@$USER.timer``

The configuration can be accessed at any time by running ``linux-ck-autobuild -c`` from a command line.
