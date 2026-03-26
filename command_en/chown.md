chown
===

Used to change the owner or group ownership of files or directories

## Description

The **chown command** changes the owner and group of a file or directory. This command can authorize a user to become the owner of a specified file or change the group the file belongs to. The user can be a username or a user ID, and the group can be a group name or a group ID. The filename can be a space-separated list of files and can include wildcards.

Only the owner of the file and the superuser can use this command.

### Syntax

```shell
chown [options] [arguments]
```

### Options

```shell
-c or --changes: Like verbose but report only when a change is made.
-f or --quiet or --silent: Suppress most error messages.
-h or --no-dereference: Affect symbolic links instead of any referenced file.
-R or --recursive: Change files and directories recursively.
-v or --verbose: Output a diagnostic for every file processed.
--dereference: Same as -h (Note: in some versions --dereference means follow symlinks).
--help: Online help.
--reference=<reference_file_or_directory>: Use the owner and group of the reference file/directory for the target.
--version: Display version information.
```

### Arguments

User:Group: Specify the owner and group. If ":Group" is omitted, only the owner is changed.
File: Specify the list of files to change. Supports multiple files, directories, and shell wildcards.

### Examples

Change the owner of the directory `/usr/meng` and all its contents to `liu`:

```shell
chown -R liu /usr/meng
```
