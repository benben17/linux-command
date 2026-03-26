rmdir
===

Used to delete empty directories.

## Description

The **rmdir command** is used to delete empty directories. When a directory is no longer in use, or when disk space reaches its limit, directories that have lost their value need to be deleted. The `rmdir` command can delete one or more empty subdirectories from a directory. The command deletes one or more subdirectories, where `dirname` represents the directory name. If no path is specified in `dirname`, the directory named `dirname` in the current directory is deleted; if `dirname` contains a path, the directory at the specified location is deleted. To delete a directory, you must have write permission for its parent directory.

Note: A subdirectory must be empty before it is deleted. This means all files in that directory must be removed using the `rm` command first. Additionally, the current working directory must be above the directory being deleted; it cannot be the directory itself or a subdirectory of it.

Although the `rm` command with the `-r` option can be used to recursively delete all files in a directory and the directory itself, doing so is very dangerous.

### Syntax 

```shell
rmdir(options)(parameters)
```

### Options 

```shell
-p or --parents: After deleting the specified directory, if its parent directory also becomes empty, delete it as well.
--ignore-fail-on-non-empty: This option causes the rmdir command to ignore error messages resulting from attempting to delete a non-empty directory.
-v or --verbose: Displays detailed information during command execution.
--help: Displays help information for the command.
--version: Displays version information for the command.
```

### Parameters 

Directory list: A list of empty directories to be deleted. When deleting multiple empty directories, separate the directory names with spaces.

### Examples 

Delete the subdirectory named `www` in the current directory:

```shell
rmdir www
```

Delete the subdirectory named `Test` in the `www` directory of the current directory. If `www` becomes empty after `Test` is deleted, `www` is also deleted.

```shell
rmdir -p www/Test
```

The following command is equivalent to `rmdir a/b/c`, `rmdir a/b`, `rmdir a`:

```shell
rmdir -p a/b/c
```
