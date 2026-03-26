swapoff
===

Disable devices and files for paging and swapping

## Description

The **swapoff command** is used to disable specified swap spaces (including swap files and swap partitions). `swapoff` is actually a symbolic link to `swapon`, used to turn off the system's swap areas.

### Syntax

```shell
swapoff (options) (parameters)
```

### Options

```shell
-a: Disable all swap spaces specified in the configuration file "/etc/fstab".
```

### Parameters

Swap space: Specify the swap space to be deactivated, which can be a swap file or a swap partition. If it is a swap partition, specify the device file corresponding to the partition.

### Examples

Disable a swap partition:

```shell
swapoff /dev/sda2
```
