uname
===

Print system information.

## Synopsis

```shell
uname [OPTION]...
```

## Main Uses

- Print information about the machine and operating system.
- When no options are provided, the `-s` option is enabled by default.
- If multiple options are given or the `-a` option is used, the output information is sorted by the following fields: kernel name, host name, kernel release, kernel version, machine name, processor, hardware platform, operating system.

## Options

```shell
-a, --all                  Print all information in order. If -p and -i information is unknown, they are omitted.
-s, --kernel-name          Print the kernel name.
-n, --nodename             Print the network node hostname.
-r, --kernel-release       Print the kernel release.
-v, --kernel-version       Print the kernel version.
-m, --machine              Print the machine name.
-p, --processor            Print the processor name.
-i, --hardware-platform    Print the hardware platform name.
-o, --operating-system     Print the operating system name.
--help                     Display help information and exit.
--version                  Display version information and exit.
```

## Return Value

Returns 0 on success, and a non-zero value on failure.

## Examples

```shell
# Using the uname command alone is equivalent to uname -s
[root@localhost ~]# uname
Linux
```

```shell
# View all information
[root@localhost ~]# uname -a
Linux localhost 2.6.18-348.6.1.el5 #1 SMP Tue May 21 15:34:22 EDT 2013 i686 i686 i386 GNU/Linux
```

```shell
# List information separately
[root@localhost ~]# uname -m
i686

[root@localhost ~]# uname -n
localhost

[root@localhost ~]# uname -r
2.6.18-4-686

[root@localhost ~]# uname -s
Linux

[root@localhost ~]# uname -v
#1 SMP Tue May 21 15:34:22 EDT 2013

[root@localhost ~]# uname -p
i686

[root@localhost ~]# uname -i
i386

[root@localhost ~]# uname -o
GNU/Linux
```

### Note

1. This command is part of the `GNU coreutils` package. For related help information, please see `man -s 1 uname` or `info coreutils 'uname invocation'`.
