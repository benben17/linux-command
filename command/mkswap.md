mkswap
===

Set up a Linux swap area

## Description

The **mkswap command** is used to set up a Linux swap area on a device or in a file. After creating the swap area, use the `swapon` command to start using it. While an optional parameter allows specifying the swap area size, it is provided for backward compatibility and is usually unnecessary, as the command defaults to using the entire device or file.

### Syntax

```shell
mkswap [OPTION]... DEVICE [SIZE]
```

### Options

```shell
-c：Check for bad blocks before creating the swap area.
-f：Force execution. Required when creating a swap area on SPARC machines.
-v0：Create an old-style swap area (default).
-v1：Create a new-style swap area.
```

### Parameters

Device: The device file or regular file to be used as swap space.

### Examples

**Check system swap space size:**

```shell
free -m
```

**View current swap space (files/partitions):**

```shell
swapon -s
# or
cat /proc/swaps
```

**Add swap space**

You can add a **swap partition** or a **swap file**. A partition is generally recommended, but a file is useful if you have limited free space.

**Steps to add a swap partition:**

1. Use `fdisk` to create a partition (e.g., `/dev/sdb2`).
2. Set up the swap area:
```shell
mkswap /dev/sdb2
```
3. Enable the swap partition:
```shell
swapon /dev/sdb2
```
4. Add it to `/etc/fstab` to enable it at boot:
```shell
/dev/sdb2 swap swap defaults 0 0
```

**Steps to add a swap file:**

1. Create a 512MB file:
```shell
dd if=/dev/zero of=/swapfile1 bs=1024 count=524288
```
2. Set up the swap file:
```shell
mkswap /swapfile1
```
3. Enable the swap file:
```shell
swapon /swapfile1
```
4. Add it to `/etc/fstab`:
```shell
/swapfile1 swap swap defaults 0 0
```

After adding and enabling the swap space, verify it using `free -m` or `cat /proc/swaps`.

**Remove swap space:**

1. Disable the swap area:
```shell
swapoff /dev/sdb2
```
2. Remove the corresponding entry from `/etc/fstab`.
3. Use `fdisk` or other tools to delete the partition or `rm` to delete the swap file.
