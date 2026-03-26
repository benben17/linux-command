chgrp
===

Used to change the group ownership of files or directories

## Description

The **chgrp command** is used to change the group that a file or directory belongs to. The group name can be the group ID or the group name. The file name can be a space-separated list of files or a collection of files described by wildcards. If the user is not the owner of the file or the superuser (root), they cannot change the group of the file.

In the UNIX family of systems, file or directory permissions are managed by the owner and the group. You can use the `chgrp` command to change the group ownership of files and directories, using either the group name or the group ID.

### Syntax

```shell
chgrp [options] [group] [file|directory]
```

### Options

```shell
-R Recursively change the group of the specified directory and all its subdirectories and files.
-c or --changes: Similar to "-v", but only reports when a change is made.
-f or --quiet or --silent: Do not display error messages.
-h or --no-dereference: Affect symbolic links instead of any referenced file.
-H If a command line argument is a symbolic link to a directory, traverse it.
-R or --recursive: Recursive processing, processing all files and subdirectories under the specified directory.
-L Traverse every symbolic link to a directory encountered.
-P Do not traverse any symbolic links (default).
-v or --verbose: Output a diagnostic for every file processed.
--reference=<reference_file_or_directory>: Set the group of the specified file or directory to match that of the reference file or directory.
```

### Arguments

* Group: Specify the new group name.
* File: Specify the list of files to change the group ownership for. Multiple files or directories are separated by spaces.

### Examples

Change the group of all files in `/usr/meng` and its subdirectories to `mengxin`:

```shell
chgrp -R mengxin /usr/meng
```

Change the group owner of file `ah` to `newuser`:

```shell
[root@rhel ~]# chgrp newuser ah
```
