runlevel
===

Print the current runlevel of the Linux system.

## Description

The **runlevel command** is used to print the current runlevel of the Linux system.

### Syntax

```shell
runlevel
```

### Knowledge Expansion

A Linux operating system goes through several different stages from the start of the boot process until it is fully started. These stages are called runlevels. Similarly, when a Linux operating system shuts down, it also goes through several other runlevels. Below we will introduce runlevels in detail and show you some tips to avoid unnecessary reboots of your Linux system.

A runlevel can be thought of as a system state. More vividly, you can think of runlevels as something like Normal, Safe Mode, and Command Prompt Only in Microsoft Windows. Entering each runlevel requires starting or stopping a corresponding series of services. These services are placed as initialization scripts in the directory `/etc/rc.d/rc?.d/` or `/etc/rc?.d/` (where `?` represents the corresponding index of the runlevel).

In most Linux distributions, there are usually 8 runlevels:

```shell
0 Halt
1 Single-user mode
2 Multi-user, without NFS
3 Full multi-user mode
4 Unused
5 Graphical interface
6 Reboot
S s Single-user mode
```

The default runlevel for most desktop Linux systems is 5 (graphical interface), while most server versions default to 3 (character interface). Runlevels 1 and 2 are rarely used except for debugging. Runlevels `s` and `S` are not intended for direct user use but rather for preparing for Single-user mode.

The advantage of Linux's running modes over Windows boot modes is that you can use the `init` command to switch between runlevels while the system is running. Furthermore, when you shut down or start the Linux system, you are unknowingly switching runlevels; the system shutdown process calls runlevel 0 or 6 to stop all running processes.
