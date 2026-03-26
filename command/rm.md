rm
===

Used to delete given files and directories.

## Description

The **rm command** can delete one or more files or directories from a directory, and it can also delete a directory along with all its files and subdirectories. For symbolic links, only the link file is deleted, while the original file remains unchanged.

Note: Use the `rm` command with extreme caution. Once a file is deleted, it cannot be recovered. Therefore, before deleting a file, it is best to check its content to ensure you really want to delete it. The `rm` command can use the `-i` option, which is particularly useful when deleting multiple files using wildcards. With this option, the system will ask you to confirm each deletion. You must enter `y` and press Enter to delete the file. If you just press Enter or any other character, the file will not be deleted.

### Syntax

```shell
rm (options)(parameters)
```

### Options

```shell
-d: Directly deletes the hard link data of the directory to be deleted to 0, thereby deleting the directory.
-f: Forcibly deletes files or directories.
-i: Prompts the user for confirmation before deleting existing files or directories.
-r or -R: Recursive processing; handles all files and subdirectories within the specified directory.
--preserve-root: Do not perform recursive operations on the root directory.
-v: Displays detailed information during command execution.
```

### Parameters

File: Specifies the list of files to be deleted. If the parameters include a directory, the `-r` or `-R` option must be used.

### Examples

Interactively delete files `test` and `example` in the current directory:

```shell
rm -i test example
Remove test ?n (do not delete file test)
Remove example ?y (delete file example)
```

Delete all files and subdirectories in the current directory except hidden files:

```shell
# rm -r *
```

Note: This is very dangerous!

**Delete the `package-lock.json` file in the current directory:**

```shell
find . -name "package-lock.json" -exec rm -rf {} \;
```

**Find files ending in `.html` and delete them:**

```shell
find ./docs -name "*.html" -exec rm -rf {} \;
```

**Delete files ending in `.html` in the current project:**

```shell
rm -rf *.html
```

**Delete the `node_modules` directory in the current directory:**

```shell
find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +
```

**Delete files:**

```shell
# rm file1 file2 ...
rm testfile.txt
```

**Delete directories:**

> rm -r [directory_name]
> -r means recursively delete all files and directories within the directory.
> -f means force delete.

```shell
rm -rf testdir
rm -r testdir
```

**Confirmation prompt before deletion:**

> rm -i [file/directory]

```shell
rm -r -i testdir
```

**Batch delete `data` folders within subfolders of the `icons` folder:**

```shell
rm -rf icons/**/data
```

**rm ignores non-existent files or directories:**

> The `-f` option (force) ensures the operation is executed, ignoring error prompts.

```shell
rm -f [file...]
```

**Confirm deletion only in certain scenarios:**

> The `-I` option ensures a confirmation prompt is shown only when deleting more than 3 files or when deleting recursively (e.g., deleting a directory).

```shell
rm -I file1 file2 file3
```

**Delete the root directory:**

> Deleting the root directory (`/`) is an operation Linux users most want to avoid, which is why the `rm` command does not support recursive deletion on the root directory by default.
> However, if you must perform this operation, you need the `--no-preserve-root` option. When this option is provided, `rm` does not treat the root directory (`/`) specially.

```shell
No example provided; deleting the operating system is not recommended! 😆
```

**rm displays details of the current deletion operation:**

```shell
rm -v [file/directory]
```
