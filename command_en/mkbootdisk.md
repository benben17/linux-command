mkbootdisk
===

Create a standalone boot disk for the current system

## Description

The **mkbootdisk command** is used to create a standalone boot floppy disk for the currently running system. This allows the system to be started and repaired in case of a boot failure.

### Syntax

```shell
mkbootdisk [OPTION]... [KERNEL_VERSION]
```

### Options

```shell
--device <device>：Specify the device to write the boot image to.
--mkinitrdargs <args>：Pass additional arguments to `mkinitrd`.
--noprompt：Do not prompt the user to insert a disk.
--verbose：Display detailed information during execution.
--version：Display version information.
```

### Parameters

Kernel Version: Specify the kernel version to use for the boot disk.

### Examples

Create a boot disk for the currently running kernel:

```shell
mkbootdisk --device /dev/fd0 `uname -r`
```

If multiple kernel versions are installed, you can specify one explicitly:

```shell
mkbootdisk --device /dev/fd0 2.2.18
```
