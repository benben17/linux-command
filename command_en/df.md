df
===

Display information about disk space usage.

## Description

The **df** command is used to display the amount of available disk space on file systems. By default, the display unit is KB. This command can be used to obtain information such as how much space is occupied on the hard disk and how much space is currently left.

### Syntax

```shell
df (options) (parameters)
```

### Options

```shell
-a, --all             Include all file systems.
--block-size=<SIZE>   Use SIZE-byte blocks.
-h, --human-readable  Print sizes in human readable format (e.g., 1K 234M 2G).
-H, --si              Likewise, but use powers of 1000 not 1024.
-i, --inodes          List inode information instead of block usage.
-k, --kilobytes       Like --block-size=1K.
-l, --local           Limit listing to local file systems.
-m, --megabytes       Like --block-size=1M.
--no-sync             Do not invoke sync before getting usage info (default).
-P, --portability     Use the POSIX output format.
--sync                Invoke sync before getting usage info.
-t, --type=<TYPE>     Limit listing to file systems of type TYPE.
-T, --print-type      Print file system type.
-x, --exclude-type=<TYPE> Limit listing to file systems not of type TYPE.
--help                Display help.
--version             Display version information.
```

### Parameters

File: Specifies a file on the file system to check.

### Size Format

Displayed values are in units of the first available `SIZE` from `--block-size`, and the `DF_BLOCK_SIZE`, `BLOCK_SIZE` and `BLOCKSIZE` environment variables. Otherwise, units default to `1024` bytes (or `512` if `POSIXLY_CORRECT` is set).

SIZE is an integer and optional unit (example: 10M is 10 * 1024 * 1024). Units are K, M, G, T, P, E, Z, Y (powers of 1024) or KB, MB, ... (powers of 1000).

### Examples

View system disk devices, default is in KB:

```shell
[root@LinServ-1 ~]# df
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2            146294492  28244432 110498708  21% /
/dev/sda1              1019208     62360    904240   7% /boot
tmpfs                  1032204         0   1032204   0% /dev/shm
/dev/sdb1            2884284108 218826068 2518944764   8% /data1
```

Use the `-h` option to display in units larger than KB for better readability:

```shell
[root@LinServ-1 ~]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda2             140G   27G  106G  21% /
/dev/sda1             996M   61M  884M   7% /boot
tmpfs                1009M     0 1009M   0% /dev/shm
/dev/sdb1             2.7T  209G  2.4T   8% /data1
```

View all file systems:

```shell
[root@LinServ-1 ~]# df -a
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2            146294492  28244432 110498708  21% /
proc                         0         0         0   -  /proc
sysfs                        0         0         0   -  /sys
devpts                       0         0         0   -  /dev/pts
/dev/sda1              1019208     62360    904240   7% /boot
tmpfs                  1032204         0   1032204   0% /dev/shm
/dev/sdb1            2884284108 218826068 2518944764   8% /data1
none                         0         0         0   -  /proc/sys/fs/binfmt_misc
```

Show the amount of available space in the `public` directory:

```shell
df public
# Filesystem     1K-blocks     Used Available Use% Mounted on
# /dev/loop0      18761008 15246924   2554392  86% /d Avail
```
