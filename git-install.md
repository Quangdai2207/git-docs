# CAI DAT GIT

Neu chi muon cac cong cu Git don gian bang file chuong trinh binary, co the thuc hien cac lenh cai dat sau cho tung he dieu hanh

- [linux](#1-linux)
- [macOs](#macos)
- [Windows](#3-windows)

## 1. Linux

Vi he dieu hanh Linux co nhieu ban phoi, lua chon 1 trong ban phoi va cach thuc cai dat phu ho cho tung ban phoi

````text
It is easiest to install Git on Linux with your distribution's package manager.

Debian/Ubuntu
For the latest stable version for your release of Debian/Ubuntu

$ apt-get install git
For Ubuntu, this PPA provides the latest stable upstream Git version

$ add-apt-repository ppa:git-core/ppa
$ apt update; apt install git
Fedora
$ yum install git (up to Fedora 21)
$ dnf install git (Fedora 22 and later)
Gentoo
$ emerge --ask --verbose dev-vcs/git
Arch Linux
$ pacman -S git
openSUSE
$ zypper install git
Mageia
$ urpmi git
Nix/NixOS
$ nix-env -i git
FreeBSD
$ pkg install git
Solaris 9/10/11 (OpenCSW)
$ pkgutil -i git
Solaris 11 Express, OpenIndiana
$ pkg install developer/versioning/git
OpenBSD
$ pkg_add git
Alpine
$ apk add git
Red Hat Enterprise Linux, Oracle Linux, CentOS, Scientific Linux, et al.
RHEL and derivatives typically ship older versions of git. You can download a 
tarball and build from source, or use a 3rd-party repository such as the IUS Community Project 
to obtain a more recent version of git.

Slitaz
$ tazpkg get-install git
````

## MacOs

```text
Mot so cach cai dat GIT cho may MacOS, co the chon mot trong so cac cach sau de cai dat

Homebrew
Install homebrew if you don't already have it, then:
$ brew install git

MacPorts
Install MacPorts if you don't already have it, then:
$ sudo port install git

Xcode Command Line Tools
Apple ships a binary package of Git with Xcode Command Line Tools. You can install this via:
$ xcode-select --install

Binary installer
Tim Harper provided an installer for Git until version 2.33.0 / 2021. These installers are no longer 
linked from here because there are no updates since that version, nor are there plans to provide any.

Installing git-gui
If you would like to install git-gui and gitk, git's commit GUI and interactive history browser, 
you can do so using homebrew
$ brew install git-gui
```

## 3. Windows

Co the vao trang chinh thuc cua Git de xem them huong dan chi tiet cai dat cho Windows.
link: [https://git-scm.com/install/windows](https://git-scm.com/install/windows "Click on")
