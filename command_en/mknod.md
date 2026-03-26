mknod
===

Create character or block special device files

## Description

The **mknod command** is used to create special device files (character or block) in the Linux filesystem.

### Syntax

```shell
mknod [OPTION]... NAME TYPE [MAJOR MINOR]
```

### Options

```shell
-Z：Set the SELinux security context.
-m, --mode=MODE：Set file permissions (mode).
--help：Display help information.
--version：Display version information.
```

### Parameters

*   Name: The filename of the device file to be created.
*   Type: The type of device file (`b` for block, `c` or `u` for character, `p` for FIFO).
*   Major: The major device number.
*   Minor: The minor device number.

### Examples

```shell
# List existing USB tty devices
ls -la /dev/ttyUSB*
crw-rw---- 1 root dialout 188, 0 2008-02-13 18:32 /dev/ttyUSB0

# Create a new character device file
mknod /dev/ttyUSB32 c 188 32
```

### Knowledge Expansion

In Linux, device management is tightly integrated with the filesystem. Devices are represented as files in the `/dev` directory. Applications can interact with hardware by opening, reading, and writing to these device files, just like regular files.

Devices are identified by a major number and a minor number. The major number identifies the device driver or type of device (e.g., hard disks typically have major number 3), while the minor number distinguishes between specific devices of that type.

Linux provides a uniform interface for all device files through the `struct file_operations` data structure, which contains pointers to functions like `open()`, `read()`, and `write()`. This abstraction allows applications to treat hardware devices and regular files identically at the I/O layer.
