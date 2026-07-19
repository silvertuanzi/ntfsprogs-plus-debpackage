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
	sudo apt install build-essential debhelper automake autoconf libtool pkgconf libgcrypt20-dev libgnutls28-dev libhd-dev libblkid-dev libgpg-error-dev uuid-dev
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

## NTFS-3G Compatibility

Since this package declares `Provides: ntfs-3g`, it includes several compatibility wrappers for legacy software that expect the original `ntfs-3g` package:

1. `ntfsfix -> fsck.ntfs`: Provides an alias for `fsck.ntfs` to repair NTFS filesystems.
2. `mount.ntfs-3g`: A compatibility wrapper that forwards to `mount -t ntfs`. This allows legacy applications that invoke `mount -t ntfs-3g` to use the system's configured `ntfs` filesystem implementation. If the [new NTFS driver](https://github.com/namjaejeon/linux-ntfs) is available (either built into Linux kernel 7.1+ or installed through [my DKMS package](https://github.com/silvertuanzi/linux-ntfs-dkms-deb)), it will be used. Otherwise, the behavior follows the kernel's handling of the `ntfs` filesystem type, which may use the legacy read-only NTFS driver or another implementation depending on the kernel configuration.
3. `mount.lowntfs-3g`: A symbolic link to the `mount.ntfs-3g` compatibility wrapper.

These wrappers are provided for compatibility with legacy software and are not intended for direct interactive use.
