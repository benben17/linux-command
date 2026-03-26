blkid
===

Locate/print block device attributes (file system type, LABEL, UUID, etc.).

## Description

In Linux, the **blkid command** can be used to query the file system type used on a device. `blkid` is primarily used to query information such as the file system type, LABEL, and UUID used by the system's block devices (including swap partitions). To use this command, the `e2fsprogs` package must be installed.

### Syntax

```shell
blkid -L | -U
blkid [-c <file>] [-ghlLv] [-o <format>] [-s <tag>] [-t <token>] [-w <file>] [<dev> ...]
blkid -p [-s <tag>] [-O <offset>] [-S <size>] [-o <format>] <dev> ...
blkid -i [-s <tag>] [-o <format>] <dev> ...
```

### Options

```shell
-c <file>   # Specify a cache file (default: /etc/blkid.tab, /dev/null = none)
-d          # Don't encode non-printing characters
-h          # Display help information
-g          # Garbage collect the blkid cache
-o <format> # Specify the output format
-k          # List all known filesystems/RAIDs and exit
-s <tag>    # Display specified information, defaults to all information
-t <token>  # Find device with a specific token (NAME=value pair)
-l          # Look up only the first device with the token specified by -t
-L <label>  # Convert LABEL to device name
-U <uuid>   # Convert UUID to device name
-v          # Display version information
-w <file>   # Write cache to a different file (/dev/null = no write)
<dev>       # Specify device(s) to probe (default: all devices)

Low-level probing options:
-p          # Low-level superblocks probing (bypass cache)
-i          # Gather information about I/O limits
-S <size>   # Overwrite device size
-O <offset> # Probe at the given offset
-u <list>   # Filter by "usage" (e.g., -u filesystem,raid)
-n <list>   # Filter by filesystem type (e.g., -n vfat,ext3)
```

### Examples

1. List the types of all mounted file systems in the current system:

```shell
sudo blkid
```

2. Display the UUID of a specified device:

```shell
sudo blkid -s UUID /dev/sda5
```

3. Display the UUIDs of all devices:

```shell
sudo blkid -s UUID
```

4. Display the LABEL of a specified device:

```shell
sudo blkid -s LABEL /dev/sda5
```

5. Display the LABELs of all devices:

```shell
sudo blkid -s LABEL
```

6. Display the file system type of all devices:

```shell
sudo blkid -s TYPE
```

7. Display all devices:

```shell
sudo blkid -o device
```

8. View detailed information in list format:

```shell
sudo blkid -o list
```
