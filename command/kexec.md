kexec
===

Directly boot into a new kernel from the currently running kernel

## Description

The **kexec** command is a patch for the Linux kernel that allows you to boot directly into a new kernel from the currently running kernel. In the boot sequence described above, kexec skips the entire bootloader stage (the first part) and jumps directly to the kernel we want to boot. There is no hardware reboot, no firmware operations, and no bootloader involvement. It completely bypasses the weakest link in the boot sequence -- the firmware. The greatest benefit of this feature is that the system can now reboot extremely fast.

**Benefits of kexec:** Systems requiring high availability, as well as kernel developers who need to constantly reboot the system, will benefit from kexec. Because kexec skips the most time-consuming part of the system reboot process (the phase where the firmware initializes hardware devices), reboots become very fast and availability is improved.

### Syntax

```shell
kexec (options)
```

### Options

```shell
-l: Specify the kernel image file;
-e: Execute the currently loaded kernel;
-f: Force an immediate call to the "kexec" system call without calling "shutdown";
-t: Specify the type of the new kernel;
-u: Unload the current kexec target kernel.
```
