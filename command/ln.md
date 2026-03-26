ln
===

Create links between files

## Description

The **ln** command is used to create links between files. There are two types of links: hard links and symbolic links (also known as soft links). By default, `ln` creates hard links. To create a symbolic link, the `-s` option must be used.

Note: A symbolic link is not an independent file; many of its attributes depend on the source file. Therefore, setting access permissions for a symbolic link file is generally meaningless.

### Syntax

```shell
ln [options]... [-T] target link_name    (1st format)
ln [options]... target                  (2nd format)
ln [options]... target... directory      (3rd format)
ln [options]... -t directory target...   (4th format)
```

### Options

```shell
--backup[=CONTROL]      # Create a backup for each existing destination file
-b                      # Like --backup but does not accept an argument
-d, -F, --directory     # Allow the superuser to attempt to hard link directories
-f, --force             # Remove existing destination files
-i, --interactive       # Prompt whether to remove destinations
-L, --logical           # Dereference targets that are symbolic links
-n, --no-dereference    # Treat LINK_NAME as a normal file if it is a symbolic link to a directory
-P, --physical          # Make hard links directly to symbolic links
-r, --relative          # Create symbolic links relative to link location
-s, --symbolic          # Make symbolic links instead of hard links
-S, --suffix=SUFFIX     # Override the usual backup suffix (default is ~)
-t, --target-directory=DIRECTORY # Specify the DIRECTORY in which to create the links
-T, --no-target-directory   # Treat LINK_NAME as a normal file always
-v, --verbose           # Print name of each linked file
--help      # Display this help and exit
--version   # Output version information and exit
```

### Parameters

*   Source file: Specify the source file for the link. If creating a symbolic link with `-s`, the source can be a file or a directory. When creating a hard link, the source must be a file.
*   Target file: Specify the name/location of the link to be created.

```shell
# CONTROL argument for --backup:
none, off       # Never make backups (even if --backup is given)
numbered, t     # Make numbered backups
existing, nil   # Numbered if numbered backups exist, simple otherwise
simple, never   # Always make simple backups
```

### Examples

Link the file `m2.c` in `/usr/mengqc/mub1` to `a2.c` in `/usr/liu`:

```shell
cd /usr/mengqc
ln mub1/m2.c /usr/liu/a2.c
```

Before execution, `a2.c` does not exist in `/usr/liu`. After execution, `a2.c` appears as a link to `m2.c` (physically they are the same file). You can see the link count increase using `ls -l`.

**Creating a symbolic link**

Create a symbolic link `abc` in `/usr/liu` pointing to the directory `/usr/mengqc/mub1`:

```shell
ln -s /usr/mengqc/mub1 /usr/liu/abc
```

**Creating a hard link**

Create a hard link `ln2022` for the file `log2022.log`. Both files will share the same attributes and data:

```shell
ln log2022.log ln2022
```

Output:

```
[root@localhost test]# ll
lrwxrwxrwx 1 root root     11 12-07 16:01 link2013 -> log2022.log
-rw-r--r-- 1 root bin      61 11-13 06:03 log2022.log
[root@localhost test]# ln log2022.log ln2022
[root@localhost test]# ll
lrwxrwxrwx 1 root root     11 12-07 16:01 link2013 -> log2022.log
-rw-r--r-- 2 root bin      61 11-13 06:03 ln2022
-rw-r--r-- 2 root bin      61 11-13 06:03 log2022.log
```

## Extended Knowledge

Linux allows multiple names for a single file, a feature known as linking. Linked files can reside in the same directory but must have different names, avoiding redundant backups on the disk. They can also have the same name if placed in different directories; modifying one will affect all others since they point to the same data. Different access permissions can be assigned to different links to control sharing and security.

There are two types of links: hard links and symbolic links.

The `ln` command creates a synchronous link in another location. When the same file is needed in different directories, there's no need to store multiple copies; just store the file once and use `ln` to link to it elsewhere, saving disk space.

> :warning: The `ln` command maintains synchronicity across all linked files; changes made to one will be reflected in all others.

### Symbolic Links (Soft Links):

1. A symbolic link exists as a path string, similar to a shortcut in Windows.
2. Symbolic links can cross file systems, whereas hard links cannot.
3. A symbolic link can point to a non-existent filename.
4. Symbolic links can point to directories.

### Hard Links

Creating a hard link adds a directory entry in the same or another directory pointing to the same file data.

1. A hard link exists as a file replica but does not occupy additional data space.
2. Hard links cannot be created for directories.
3. Hard links can only be created within the same file system.

```shell
ls -ailR
.:
total 16
922730 drwxr-xr-x  4 root root 4096 Jun 17 11:18 .
393217 drwxrwxrwt. 9 root root 4096 Jun 17 11:19 ..
922733 drwxr-xr-x  2 root root 4096 Jun 17 11:18 liu
922731 -rw-r--r--  3 root root    0 Jun 17 11:18 m2.c
922732 drwxr-xr-x  2 root root 4096 Jun 17 11:18 mub1

./liu:
total 8
922733 drwxr-xr-x 2 root root 4096 Jun 17 11:18 .
922730 drwxr-xr-x 4 root root 4096 Jun 17 11:18 ..
922731 -rw-r--r-- 3 root root    0 Jun 17 11:18 m2.c

./mub1:
total 8
922732 drwxr-xr-x 2 root root 4096 Jun 17 11:18 .
922730 drwxr-xr-x 4 root root 4096 Jun 17 11:18 ..
922731 -rw-r--r-- 3 root root    0 Jun 17 11:18 m2.c
```

After creating hard links, the inode number of the existing file is shared by multiple directory entries. The link count is shown in the second column of the `ls -l` output.

By default, `ln` creates hard links. `ln` increases the link count, while `rm` decreases it. A file is not physically deleted from the file system until its link count reaches zero.

Restrictions on hard links:
* Cannot be created for directories.
* Cannot cross file system boundaries.

### Symbolic Links (Soft Links) - Technical Details

A symbolic link links a path name to a file. It is a special type of file that contains the path name of another file. When commands read or write to a symbolic link, the system follows the link to access the actual file.

```shell
$ ls -il
total 0
922736 lrwxrwxrwx 1 root root 5 Jun 17 11:27 abc -> a.txt
922735 -rw-r--r-- 1 root root 0 Jun 17 11:27 a.txt
```

Unlike hard links, a symbolic link is a new file with its own inode. It does not have the restrictions of hard links: it can point to directories and cross file systems.

When creating a symbolic link with `ln -s`, it is recommended to use absolute paths for the source to ensure the link works regardless of the current working directory.

Key characteristics of symbolic links:
* Deleting the source file breaks the link (it becomes "dangling"), but the link file remains.
* In directory listings, symbolic links are indicated by the letter `l` as the first character of the permissions string.
* The size of a symbolic link file is the number of bytes in the path name it points to.
* `ls -l` shows the link target with an arrow (e.g., `abc -> a.txt`).
