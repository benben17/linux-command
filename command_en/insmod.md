insmod
===

Insert a module into the Linux kernel.

## Description

The `insmod` command is used to load a specified module into the kernel. Many Linux features are implemented as modules and loaded into the kernel only when needed. This keeps the kernel lean and efficient while maintaining flexibility. These loadable modules are typically device drivers.

### Syntax

```shell
insmod [options] [filename]
```

### Options

```shell
-f : Force loading of the module even if the kernel version doesn't match the version the module was compiled for.
-k : Set the module to be auto-removable.
-m : Output module loading information.
-o <name> : Specify the name of the module.
-p : Test if the module can be loaded correctly into the kernel.
-s : Log all messages to the system log.
-v : Enable verbose mode.
-x : Do not export external symbols from the module.
-X : Export all external symbols (default).
```

### Parameters

Kernel module: The path to the kernel module file (.ko) to be loaded.

### Examples

Load the RAID1 module:

```shell
[root@localhost boot]# insmod /lib/modules/$(uname -r)/kernel/drivers/md/raid1.ko  

[root@localhost boot]# lsmod | grep raid1
raid1                  25153  0
```

The output shows that the RAID1 module was loaded successfully. Note that `insmod` requires an absolute path and does not automatically resolve module dependencies (use `modprobe` for dependency resolution).
