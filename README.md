# WoeUSB
[![Latest Release](https://img.shields.io/github/release/slacka/WoeUSB.svg)](https://github.com/slacka/WoeUSB/releases)
[![WoeUSB License](https://img.shields.io/badge/license-gpl-blue.svg)](https://github.com/slacka/WoeUSB/blob/master/COPYING)
[![Build Status](https://travis-ci.org/slacka/WoeUSB.svg?branch=master)](https://travis-ci.org/slacka/WoeUSB)

![brand](src/data/woeusb-logo.png)[![thumbnail of GUI wrapper screenshot](dev/woeusbgui-screenshot.thumbnail.png)](dev/woeusbgui-screenshot.png)[![thumbnail of CLI application screenshot](dev/woeusb-screenshot.thumbnail.png)](dev/woeusb-screenshot.png)

_A Linux program to create a Windows USB stick installer from a real Windows DVD or image._

This package contains two programs:

* woeusb: A command-line utility that enables you to create your own bootable Windows installation USB storage device from an existing Windows Installation disc or disk image
* woeusbgui: A GUI wrapper of woeusb based on WxWidgets

Supported images:

Windows Vista, Windows 7, Window 8.x, Windows 10. All languages and any version (home, pro...) and Windows PE are supported.

Supported bootmodes:

* Legacy/MBR-style/IBM PC compatible bootmode
* Native UEFI booting is supported for Windows 7 and later images (limited to the FAT filesystem as the target)

This project is a fork of [Congelli501's WinUSB software](http://en.congelli.eu/prog_info_winusb.html), which has not been maintained since 2012, according to the official website.

## Installation
### Prebuilt Packages
Note that prebuilt packages are not necessarily the latest release and we are NOT responsible for the trustworthiness of these packages.  Regarding any related issues contact its maintainer first.

#### Official Distribution Packages
* [Fedora](https://src.fedoraproject.org/rpms/WoeUSB) packages maintained by mprahl
* [openSUSE](https://software.opensuse.org/package/WoeUSB) packages maintained by [guoyunhe](https://guoyunhe.me/)
* [Gentoo](https://packages.gentoo.org/packages/sys-boot/woeusb) packages maintained by pacho

#### Third-party Distribution Packages
* [Arch Linux](https://aur.archlinux.org/packages/woeusb-git/) packages maintained by darkfm
* [̶U̶b̶u̶n̶t̶u̶]̶(̶h̶t̶t̶p̶s̶:̶/̶/̶l̶a̶u̶n̶c̶h̶p̶a̶d̶.̶n̶e̶t̶/̶%̶7̶E̶n̶i̶l̶a̶r̶i̶m̶o̶g̶a̶r̶d̶/̶+̶a̶r̶c̶h̶i̶v̶e̶/̶u̶b̶u̶n̶t̶u̶/̶w̶e̶b̶u̶p̶d̶8̶)̶ ̶p̶a̶c̶k̶a̶g̶e̶s̶ ̶m̶a̶i̶n̶t̶a̶i̶n̶e̶d̶ ̶b̶y̶ ̶[̶W̶e̶b̶U̶p̶d̶8̶]̶(̶h̶t̶t̶p̶:̶/̶/̶w̶w̶w̶.̶w̶e̶b̶u̶p̶d̶8̶.̶o̶r̶g̶/̶)̶
### Build from Source
The following are the instructions to install WoeUSB if prebuilt version is not available or too old.

#### Acquire WoeUSB's Source Code
Clone WoeUSB's Git repository to your local machine using `git clone https://github.com/slacka/WoeUSB.git`

NOTE: We no longer support building from source archives provided in the GitHub Releases page as the software version is not set.

#### Setting the Application Version String
This step is required for generating the proper version name based on the Git tags. This step should be repeated if the version is changed.

```shell
$ ./setup-development-environment.bash
```

#### Install WoeUSB's Build Dependencies
```shell
# For Debian-based distributions (NOTE: For your convenience, this package is already provided in the release page)
$ sudo apt-get install devscripts equivs gdebi-core
$ cd <WoeUSB source tree directory, the folder that contains the `src` folder>
$ mk-build-deps # NOTE: Currently, due to Debian Bug #679101, this command will fail if the source path contains spaces.
$ sudo gdebi woeusb-build-deps_<version>_all.deb

# For Fedora > 22
$ sudo dnf install wxGTK3-devel

# For Fedora 22
$ sudo dnf install wxGTK-devel dh-autoreconf.noarch

# For Opensuse
$ sudo zypper in wxGTK3-3_2-devel dh-autoreconf devscripts
```
#### Build & Install WoeUSB
```shell
# For Debian-based distributions
$ dpkg-buildpackage -uc -b # NOTE: Currently, due to a bug in the build system, this command will fail if the source's path contains space or single quotes, refer to issue #84 for details
$ sudo gdebi ../woeusb_<version>_<architecture>.deb

# Generic method
$ autoreconf --force --install # Most non-Debian derived distros will need this
$ ./configure
$ make
$ sudo make install
```

#### Build & Install on Debian and Ubuntu based Distros
I just thought that I would add this small tutorial that the AWESOME @Thomashighbaugh showed me, to help the users that are confused as to what to do with the source code, and how to build it. This is for Debian and Ubuntu based Distros of course


# For Debian and Ubuntu based distributions
$ sudo apt-get update 

$ sudo apt-get upgrade -y 

$ sudo apt-get install devscripts equivs gdebi-core git

$ git clone https://github.com/slacka/WoeUSB

$ cd WoeUSB  

# Run the provided script to set up the development environment
$ bash setup-development-environment.bash

# Now We Install WoeUSB's Dependencies
$ mk-build-deps # NOTE: Currently, due to Debian Bug #679101, this command
# will fail if the source path contains spaces.

# to determine the version number (replace the <version> tag below with what is displayed)
$ ls -ah

# using debian package manager
$ sudo dpkg -i woeusb-build-deps_<version>_all.deb

# using gdebi as the README suggests
$ sudo gdebi woeusb-build-deps_<version>_all.deb

# Build the DEB package
$ dpkg-buildpackage -uc -b # NOTE: Currently, due to a bug in the build system, this command 
# will fail if the source's path contains space or single quotes, refer to issue #84 for details

# The .deb will be in your home folder (if that's where you started)
$ cd ..

# Use the list command to determine the version and architecture of you deb file and replace
# <version> and <architecture> with the corresponding strings
ls -ah

# to install using the debian package manager 
dpkg -i woeusb_<version>_<architecture>.deb

# to install using gdebi
$ sudo gdebi ../woeusb_<version>_<architecture>.deb

# to remove the extra files in the working directory (though you might want to save the .deb file)
$ rm -r WoeUSB 


## License
WoeUSB is distributed under the [GPL license](https://github.com/slacka/WoeUSB/blob/master/COPYING).
