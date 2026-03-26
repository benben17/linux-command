pvchange
===

Change physical volume attributes

## Description

The **pvchange command** allows an administrator to change the allocation permissions for physical volumes. If a physical volume fails, the `pvchange` command can be used to prohibit the allocation of Physical Extents (PEs) on that volume.

### Syntax

```shell
pvchange(options)(parameters)
```

### Options

```shell
-u: Generate a new UUID;
-x: Whether to allow PE allocation.
```

### Parameters

Physical Volume: Specifies the device file for the physical volume whose attributes are to be modified.

### Example

Use the `pvchange` command to prohibit PE allocation on a specified physical volume. Enter the following command:

```shell
pvchange -x n /dev/sdb1     # Prohibit PE allocation on "/dev/sdb1"
```

Output information:

```shell
Physical volume "/dev/sdb1" changed  
1 physical volume changed / 0 physical volumes not changed
```
