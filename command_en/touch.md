touch
===

Create new empty files

## Description

The **touch command** has two main functions: first, to update the timestamps of existing files to the current system time (default behavior), leaving their data intact; second, to create new empty files.

### Syntax

```shell
touch [options] [parameters]
```

### Options

```shell
-a: or --time=atime, --time=access, --time=use. Only change the access time;
-c: or --no-create. Do not create any files;
-d: <date/time>. Use the specified date and time instead of the current time;
-f: Ignored; provided only for compatibility with BSD versions of touch;
-m: or --time=mtime, --time=modify. Only change the modification time;
-r: <reference file or directory>. Set the date and time of the specified file or directory to match those of the reference;
-t: <date/time>. Use the specified date and time (format: [[CC]YY]MMDDhhmm[.ss]) instead of the current time;
--help: Display online help;
--version: Display version information.
```

### Parameters

File: Specifies the list of files whose time attributes are to be set.

### Examples

```shell
touch ex2
```

Creates an empty file named `ex2` in the current directory. You can use the `ls -l` command to verify that the size of `ex2` is 0, indicating it is an empty file.

Create multiple files at once:

```shell
touch file{1..5}.txt
```

Create a `job1.md` file and write `job 1` into it:

```shell
echo "job 1" > job1.md
```
