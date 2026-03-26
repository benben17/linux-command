mkinitrd
===

Create an initial ramdisk image for preloading modules

## Description

The **mkinitrd command** creates an initial ramdisk image (initrd) for the Linux kernel. This image is loaded into memory at boot time and contains modules needed to mount the root filesystem (e.g., disk drivers, filesystem modules).

This is often used when a new driver is modified or added that needs to be available at the earliest stages of the boot process.

### Syntax

```shell
mkinitrd [OPTION]... IMAGE KERNEL-VERSION
```

### Options

```shell
-f：Overwrite the existing image file if it has the same name.
-v：Verbose mode; display detailed information during execution.
--omit-scsi-modules：Do not load any SCSI modules.
--preload <module>：Preload the specified module.
--with <module>：Include the specified module in the image.
--version：Display version information.
```

### Parameters

*   Image: The name of the output image file (e.g., `initrd.img`).
*   Kernel Version: The version of the kernel for which the image is created.

### Examples

Create an initrd image for the currently running kernel:

```shell
[root@localhost tmp]# mkinitrd -v -f myinitrd.img $(uname -r)
Creating initramfs
...
Using modules:  ./kernel/fs/jbd/jbd.ko ./kernel/fs/ext3/ext3.ko
...
Loading module jbd
Loading module ext3

[root@localhost tmp]# file myinitrd.img
myinitrd.img: gzip compressed data, from Unix, max compression
```
