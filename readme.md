# ntfsprogs-plus-debpackage

Debian packaging for the upstream [ntfsprogs-plus](https://github.com/ntfsprogs-plus/ntfsprogs-plus) project.

To avoid ABI compatibility issues across different Debian and Ubuntu releases, building the package from source is the recommended installation method.

For convenience, experimental prebuilt packages built on Ubuntu 22.04 are also provided in the [Releases](https://github.com/silvertuanzi/ntfsprogs-plus-debpackage/releases). Thanks to glibc's backward compatibility, they are expected to work on Ubuntu 22.04 or later and Debian 12 (Bookworm) or later, but only the Ubuntu 22.04 build environment is currently tested.

## Build

1. Clone the repository:
	```
	git clone https://github.com/silvertuanzi/ntfsprogs-plus-debpackage.git --recursive
	```
2. Install build dependencies:
	```
	sudo apt install build-essential debhelper automake autoconf libtool pkgconf libgcrypt20-dev libgnutls28-dev libhd-dev libblkid-dev
	```
3. Build the package:
	```
	cd ntfsprogs-plus-debpackage
	dpkg-buildpackage -us -uc -b
	```
4. Install it:
	```
	sudo apt install ../ntfsprogs-plus_*.deb
	```
 
