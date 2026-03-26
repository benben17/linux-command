mtools
===

Display utilities supported by mtools

## Description

The **mtools command** displays the utilities supported by `mtools`. `mtools` is a collection of utilities for accessing MS-DOS disks from Unix/Linux systems without mounting them. These commands are typically symbolic links to `mtools` and share common characteristics.

### Syntax

```shell
mtools [options]
```

### Options

```shell
-a: Automatically change the long filename of the destination file if it already exists.
-A: Automatically change the short filename of the destination file if the short filename exists but the long filename is different.
-o: Overwrite the existing file if the long filename matches.
-O: Overwrite the existing file if the short filename matches but the long filename is different.
-r: Prompt the user to rename the long filename of the destination file if it already exists.
-R: Prompt the user to rename the short filename of the destination file if the short filename exists but the long filename is different.
-s: Skip the destination file if the long filename already exists.
-S: Skip the destination file if the short filename exists but the long filename is different.
-v: Verbose mode, displays detailed information during execution.
-V: Display version information.
```

### Examples

Use the `mtools` command to display all supported utilities:

```shell
[root@localhost ~]# mtools     # Display names of all supported commands
Supported commands:
mattrib, mbadblocks, mcat, mcd, mclasserase, mcopy, mdel, mdeltree
mdir, mdoctorfat, mdu, mformat, minfo, mlabel, mmd, mmount
mpartition, mrd, mread, mmove, mren, mshowfat, mtoolstest, mtype
mwrite, mzip
```

As shown above, all these commands are part of the `mtools` suite.
