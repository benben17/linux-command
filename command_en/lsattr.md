lsattr
===

List file attributes on a Linux second extended file system

## Description

The **lsattr command** is used to view the attributes of files on a Linux second extended file system (ext2/ext3/ext4).

### Syntax

```shell
lsattr [OPTION]... [FILE]...
```

### Options

```shell
-E: Displays the current values of the device attributes.
-D: Displays the attribute name, default value, description, and a flag indicating whether the user can modify the attribute value.
-R: Recursively list attributes of directories and their contents.
-V: Display the program version.
-a: List all files in directories, including dot files.
```

The frequently used options -D, -E, and -R are mutually exclusive and cannot be used together. When using `lsattr`, a specific device name must be provided. Use the -l option to specify the logical name of the device, or use -c, -s, -t options to uniquely identify an existing device.

### Parameters

File: The file(s) for which to display file system attributes.

### Examples

```shell
lsattr -E -l rmt0 -H
lsattr -EO -l rmt0
```
