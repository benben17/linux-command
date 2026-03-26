umount
===

Unmount a filesystem

## Description

The **umount command** is used to unmount a filesystem that has already been mounted. You can unmount a filesystem using either its device name or its mount point; however, unmounting by mount point is recommended to avoid confusion when using bind mounts (where one device has multiple mount points).

### Syntax

```shell
umount [options] [parameters]
```

### Options

```shell
-a: Unmount all filesystems listed in /etc/mtab;
-h: Display help;
-n: Do not record the unmounting in /etc/mtab;
-r: If unmounting fails, attempt to remount the filesystem as read-only;
-t <fstype>: Unmount only the filesystems of the specified type;
-v: Verbose mode, displaying detailed information during execution;
-V: Display version information.
```

### Parameters

Filesystem: Specifies the filesystem to be unmounted or its corresponding device filename.

### Examples

The following two commands unmount a filesystem using the device name and the mount point, respectively, while providing detailed output:

Unmount by device name:

```shell
umount -v /dev/sda1
/dev/sda1 unmounted
```

Unmount by mount point:

```shell
umount -v /mnt/mymount/
/tmp/diskboot.img unmounted
```

If the device is busy, the unmounting will fail. A common reason for failure is an open shell whose current directory is within the mount point:

```shell
umount -v /mnt/mymount/
umount: /mnt/mymount: device is busy
umount: /mnt/mymount: device is busy
```

Sometimes it's difficult to find the reason why a device is busy. In such cases, you can use `lsof` to list open files and search the list for the mount point you're trying to unmount:

```shell
lsof | grep mymount         # Find open files in the mymount partition
bash   9341  francois  cwd   DIR   8,1   1024    2 /mnt/mymount
```

The output above shows that the `mymount` partition cannot be unmounted because a bash process with PID 9341, run by user `francois`, is using it.

Another way to handle a busy system file is to perform a lazy unmount:

```shell
umount -vl /mnt/mymount/     # Perform lazy unmount
```

A lazy unmount immediately detaches the filesystem from the directory tree and cleans up all associated resources as soon as the device is no longer busy. To unmount and eject removable storage media, use the `eject` command:

```shell
eject /dev/cdrom      # Unmount and eject CD
```
