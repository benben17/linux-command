blockdev
===

Call block device ioctls from the command line.

## Description

The **blockdev command** calls `ioctl` functions from the command line to achieve control over devices.

### Syntax

```shell
blockdev [options] [parameters]
```

### Options

```shell
-V: Print version number and exit.
-q: Quiet mode.
-v: Verbose mode.
--setro: Set read-only.
--setrw: Set read-write.
--getro: Print read-only status. "1" means read-only, "0" means not read-only.
--getss: Print sector size. Usually 512.
--flushbufs: Flush buffers.
--rereadpt: Reread partition table.
```

### Parameters

Device Filename: Specify the device filename of the disk to be operated on.

### Examples

Set a device to read-only:

```shell
blockdev --setro /dev/hda4
```

Check if a device is read-only:

```shell
blockdev --getro /dev/hda4
```

Set a device to read-write:

```shell
blockdev --setrw /dev/hda4
```
