init
===

The parent of all Linux processes.

## Description

The `init` command is the process initialization tool for Linux. The `init` process is the parent of all Linux processes and always has a Process ID (PID) of 1. It is an essential part of the Linux operating system, started by the kernel during the boot process as the very first process.

### Syntax

```shell
init [options] [runlevel]
```

### Options

```shell
-b : Boot directly into single-user mode without running scripts.
-s : Switch to single-user mode.
```

### Parameters

Runlevel: Specify the target runlevel for the system to switch to.

### Examples

Commonly used commands:

- View system processes: `ps -ef | head`
- View the init configuration: `more /etc/inittab`
- View the current runlevel: `runlevel`

#### Runlevels

A runlevel is a state of the operating system. Runlevels range from 0 to 6, each with different functions:

```shell
# 0  Halt (do NOT set initdefault to 0)
# 1  Single-user mode
# 2  Multi-user, without NFS (similar to level 3 but stops some services)
# 3  Full multi-user mode
# 4  Unused
# 5  X11 (Graphical user interface)
# 6  Reboot (do NOT set initdefault to 6)
```
