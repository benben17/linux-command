rmmod
===

Remove specified kernel modules from the running kernel.

## Description

The **rmmod command** is used to remove specified kernel modules from the currently running kernel. By executing the `rmmod` command, unnecessary modules can be deleted. The Linux kernel has modular characteristics; therefore, when compiling the kernel, it is not necessary to include all functionalities in the core. You can compile these functionalities into individual modules and load them as needed.

### Syntax

```shell
rmmod(options)(parameters)
```

### Options

```shell
-v: Displays detailed information about command execution.
-f: Forcibly removes modules; using this option is dangerous.
-w: Waits until the module can be removed before removing it.
-s: Sends error messages to the system log (syslog).
```

### Parameters

Module name: The name of the module to be removed.

### Examples

The `rmmod` command is primarily used to unload Linux kernel modules currently in use, similar to the `modprobe -r` command, as shown below:

```shell
[root@localhost boot]# lsmod | grep raid1
raid1                  25153  0

[root@localhost boot]# rmmod raid1
[root@localhost boot]# lsmod | grep raid1
```
