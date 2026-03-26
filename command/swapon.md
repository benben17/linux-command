swapon
===

Enable devices and files for paging and swapping

## Description

The **swapon command** is used to activate swap space in a Linux system. Linux memory management requires the use of swap areas to establish virtual memory.

### Syntax

```shell
swapon (options) (parameters)
```

### Options

```shell
-a: Enable all devices marked as swap in the /etc/fstab file.
-h: Display help.
-p <priority>: Specify the priority of the swap area.
-s: Display swap usage status.
-V: Display version information.
```

### Parameters

Swap space: Specify the swap space to be activated, which can be a swap file or a swap partition. If it is a swap partition, specify the device file corresponding to the partition.

### Examples

```shell
mkswap -c /dev/hdb4 (-c checks for bad blocks)
swapon -v /dev/hdb4
swapon -s
Filename                                type            Size    Used    Priority
/dev/hda5                               partition       506008 96      -1
/dev/hdb4                               partition       489972 0       -2
```
