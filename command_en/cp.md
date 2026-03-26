cp
===

Copy files and directories

## Description

The **cp command** is used to copy one or more source files or directories to a specified destination file or directory. It can copy a single source file to a specific filename or into an existing directory. The `cp` command also supports copying multiple files at once; in this case, the destination must be an existing directory, otherwise an error will occur.

### Syntax

```shell
cp [options] [arguments]
```

### Options

```shell
-a: Archive mode; same as -dpR.
-d: When copying symbolic links, create a symbolic link in the destination instead of copying the file it points to.
-f: Force copy files or directories, even if the destination exists.
-i: Prompt before overwriting existing files.
-l: Create hard links instead of copying files.
-p: Preserve file attributes (owner, group, permissions, timestamps).
-R/r: Recursive copy; process all files and subdirectories.
-s: Create symbolic links instead of copying files.
-u: Update mode; copy only when the source is newer than the destination or the destination does not exist.
-S: Use a specified "SUFFIX" for backup files.
-b: Make a backup of each existing destination file before overwriting.
-v: Verbose; explain what is being done.
```

### Arguments

*   Source: List of source files or directories. By default, `cp` cannot copy directories unless the `-R` or `-r` option is used.
*   Destination: The target file or directory. If multiple source files are specified, the destination must be a directory.

### Examples

The first example uses `cp` with multiple options (`-r` for recursive, `-u` for update, and `-v` for verbose). This is useful for copying only new files to a storage device.

Note that `-r` can also be written as `--recursive`. Short options can be combined, such as `-ruv`.

```shell
cp -r -u -v /usr/men/tmp ~/men/tmp
```

Use the `--backup=numbered` option to create numbered backups. For example, the first backup will be `.1`, the second `.2`, and so on.

```shell
$ cp --force --backup=numbered test1.py test1.py
$ ls
test1.py test1.py.~1~ test1.py.~2~
```

If you copy a file to a destination that already exists, the content of the target file will be overwritten. Both absolute and relative paths (including `.` and `..`) can be used. For example, to copy a file to the current directory:

```shell
cp ../mary/homework/assign .
```

The destination directory must already exist; `cp` cannot create directories. If you do not have permission to copy a file, an error message will be displayed.

Copy `file` to `/usr/men/tmp` and rename it to `file1`:

```shell
cp file /usr/men/tmp/file1
```

Copy all files and subdirectories from `/usr/men` to `/usr/zh`:

```shell
cp -r /usr/men /usr/zh
```

Interactively copy all `.c` files starting with `m` from `/usr/men` to `/usr/zh`:

```shell
cp -i /usr/men/m*.c /usr/zh
```

When copying files in Linux, you might want to overwrite existing files without being prompted for confirmation. If there are many files, pressing `Y` repeatedly is inefficient. Here are some ways to handle this:

```shell
cp aaa/* /bbb
# Copy everything from aaa to /bbb. If /bbb has files with the same name, you must press Y to confirm. Subdirectories in aaa are skipped.

cp -r aaa/* /bbb
# Still requires confirmation, but subdirectories are not skipped.

cp -r -a aaa/* /bbb
# Still requires confirmation; preserves directory, subdirectory, and file attributes.

\cp -r -a aaa/* /bbb
# Success! No confirmation prompts, attributes are preserved, and subdirectories are included.
```

Recursive force copy to overwrite existing files:

```shell
cp -rfb ./* ../backup
# Copy all files in the current directory to the sibling directory "backup".
```

Copy hidden files (e.g., `.babelrc`):

```shell
cp -r aaa/.* ./bbb
# Copy all hidden files starting with "." from aaa to bbb.

cp -a aaa ./bbb/ 
# Use the -a option; it's recommended to include the trailing "/" for the destination directory.
```

Copy to the current directory:

```shell
cp aaa.conf ./
# Copy aaa.conf to the current directory.
```
观察
