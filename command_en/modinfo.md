modinfo
===

Show information about a Linux kernel module

## Description

The **modinfo command** extracts and displays information from Linux kernel modules. It can show details such as the module's author, description, license, parameters, and more.

### Syntax

```shell
modinfo [OPTION]... [MODULE_NAME|FILENAME]
```

### Options

```shell
-a, --author：Display the module's author.
-d, --description：Display the module's description.
-l, --license：Display the module's license.
-p, --parameters：Display the parameters that the module accepts.
-n, --filename：Display the module's filename.
-0, --null：Use the ASCII NULL character to separate fields instead of a newline.
-F, --field <field>：Only display the value of the specified field.
```

### Parameters

Module Name: The name of the kernel module (e.g., `sg`).
Filename: The path to a module file (e.g., `/path/to/module.ko`).

### Examples

Display information for the `sg` (SCSI generic) module:

```shell
[root@localhost ~]# modinfo sg
filename:    /lib/modules/2.6.9-42.ELsmp/kernel/drivers/scsi/sg.ko
author:     Douglas Gilbert
description:  SCSI generic (sg) driver
license:    GPL
version:    3.5.31 B0B0CB1BB59F0669A1F0D6B
parm:      def_reserved_size:size of buffer reserved for each fd
parm:      allow_dio:allow direct I/O (default: 0 (disallow))
alias:     char-major-21-*
vermagic:    2.6.9-42.ELsmp SMP 686 REGPARM 4KSTACKS gcc-3.4
depends:    scsi_mod
```
