# ntfsprogs-plus-debpackage

Debian packaging for the upstream [ntfsprogs-plus](https://github.com/ntfsprogs-plus/ntfsprogs-plus) project.

To avoid ABI compatibility issues across different Debian and Ubuntu releases, this repository only contains the packaging source. Build the package locally using the steps below.

## Build

1. Clone the repository:
	```
	git clone https://github.com/silvertuanzi/ntfsprogs-plus-debpackage.git --recursive
	```
2. Install build dependencies:
	```
	sudo apt install build-essential debhelper automake autoconf libtool pkg-config libgcrypt20-dev libgnutls28-dev
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
 
