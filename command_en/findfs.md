findfs
===

Find a filesystem by label or UUID.

## Description

The **findfs command** locates a filesystem device based on its volume label or UUID. The `findfs` command searches all disks in the system to find a match. If a match is found, the device name is printed to standard output. The `findfs` command is part of the `e2fsprogs` project.

### Syntax

```shell
findfs (parameter)
```

### Parameters

`LABEL=<label>` or `UUID=<uuid>`: Query the filesystem by its volume label or UUID.

### Example

Find the device corresponding to a volume label:

```shell
findfs LABEL=/boot
/dev/hda1
```
