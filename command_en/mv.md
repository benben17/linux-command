mv
===

Used to rename or move files or directories

## Description

The **mv command** is used to rename files or directories, or to move files from one directory to another. `source` represents the source file or directory, and `target` represents the destination file or directory. If a file is moved to an existing destination file, the content of the destination file will be overwritten.

The `mv` command can be used to move a source file to a destination file, or a set of files to a destination directory. Moving a source file to a destination file has two different outcomes:

1.  If the destination is a path to a directory, the source file is moved into that directory with its filename unchanged.
2.  If the destination is not a directory, the source filename (only one source file is allowed in this case) is changed to the destination filename, overwriting any existing file with the same name. If the source and destination are in the same directory, `mv` effectively renames the file. When the destination is a directory, multiple source files or directories can be specified, and all will be moved into the destination directory, retaining their original names.

Note: Unlike `cp`, `mv` is like "moving house"; it doesn't increase the total number of files. `cp` creates a copy, so the number of files increases.

### Syntax

```shell
mv [options] source target
```

### Options

```shell
--backup=<mode>: Back up files before overwriting.
-b: Create a backup before overwriting if the file exists.
-f: Force overwrite: directly overwrite existing files or directories without prompting.
-i: Interactive mode: prompt before overwriting an existing file. Enter "y" to overwrite or "n" to cancel. This helps prevent accidental data loss.
--strip-trailing-slashes: Remove trailing slashes from source arguments.
-S <suffix>: Use the specified suffix for backup files instead of the default.
--target-directory=<directory>: Specify the destination directory to move source files into.
-u: Update: only move files that are newer than the destination or if the destination doesn't exist.
```

### Parameters

*   Source file: A list of source files or directories.
*   Target file: If "target" is a filename, the source is moved and renamed to it. If "target" is a directory name, the source is moved into that directory.

### Examples

Move all files from `/usr/men` to the current directory (`.`):

```shell
mv /usr/men/* .
```

Move a file:

```shell
mv file_1.txt /home/office/
```

Move multiple files:

```shell
mv file_2.txt file_3.txt file_4.txt /home/office/
mv *.txt /home/office/
```

Move a directory:

```shell
mv directory_1/ /home/office/
```

Rename a file or directory:

```shell
mv file_1.txt file_2.txt # Rename file_1.txt to file_2.txt
```

Rename a directory:

```shell
mv directory_1/ directory_2/
```

Print move information (verbose):

```shell
mv -v *.txt /home/office
```

Prompt before overwriting:

```shell
mv -i file_1.txt /home/office
```

Update only when source is newer than destination:

```shell
mv -uv *.txt /home/office
```

Do not overwrite any existing files:

```shell
mv -vn *.txt /home/office
```

Create backup when moving:

```shell
mv -bv *.txt /home/office
```

Unconditionally overwrite existing files:

```shell
mv -f *.txt /home/office
```
