lsblk
===

List information about block devices

## Description

The **lsblk command** lists information about all available or specified block devices. It displays dependencies between devices but does not list RAM disks. Block devices include hard drives, flash drives, CD-ROMs, etc. The `lsblk` command is part of the `util-linux` package.

### Options

```shell
-a, --all            # Display all devices.
-b, --bytes          # Print the SIZE column in bytes rather than in a human-readable format.
-d, --nodeps         # Don't print device holders or slaves.
-D, --discard        # Print information about the discarding capabilities (TRIM/UNMAP) for each device.
-e, --exclude <list> # Exclude devices by major number.
-f, --fs             # Output info about file systems.
-h, --help           # Display help information.
-i, --ascii          # Use ASCII characters for tree formatting.
-m, --perms          # Output info about device owner, group and mode.
-l, --list           # Use list output format.
-n, --noheadings     # Do not print a header line.
-o, --output <list>  # Specify which output columns to print.
-P, --pairs          # Use key="value" output format.
-r, --raw            # Use raw output format.
-t, --topology       # Output info about topology.
```

### Examples

By default, `lsblk` lists block devices in a tree-like format:

```shell
lsblk

NAME   MAJ:MIN rm   SIZE RO type mountpoint
sda      8:0    0 232.9G  0 disk 
├─sda1   8:1    0  46.6G  0 part /
├─sda2   8:2    0     1K  0 part 
├─sda5   8:5    0   190M  0 part /boot
├─sda6   8:6    0   3.7G  0 part [SWAP]
├─sda7   8:7    0  93.1G  0 part /data
└─sda8   8:8    0  89.2G  0 part /personal
sr0     11:0    1  1024M  0 rom
```

The columns are:

1.  **NAME**: Device name.
2.  **MAJ:MIN**: Major and minor device numbers.
3.  **RM**: Whether the device is removable (1 if yes).
4.  **SIZE**: Capacity of the device.
5.  **RO**: Whether the device is read-only (1 if yes).
6.  **TYPE**: Device type (e.g., disk, part, rom).
7.  **MOUNTPOINT**: Where the device is mounted.

Show all devices, including empty ones:

```shell
lsblk -a
```

Show permissions and ownership:

```shell
lsblk -m
```

Show size in bytes for a specific device:

```shell
lsblk -b /dev/sda
# or
lsblk --bytes /dev/sda
```

List format without headings:

```shell
lsblk -nl
```

List SCSI devices:

```shell
lsblk -S
```

Reverse dependency order:

```shell
lsblk -s
```
