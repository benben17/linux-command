basename
===

Strip directory and suffix from filenames.

## Description

The **basename command** is used to print the base name of a directory or file. The `basename` and `dirname` commands are commonly used for command substitution in shell scripts to specify an output filename that differs from the input filename.

### Syntax

```shell
basename [options] [parameters]
```

### Options

```shell
--help: Display help information.
--version: Display version information.
```

### Parameters

* File: A filename with path information.
* Suffix: Optional parameter, specifies the filename suffix to be removed.

### Examples

1. To display the base name of a shell variable, enter:

```shell
basename $WORKFILE
```

This command displays the base name of the value assigned to the shell variable `WORKFILE`. If the value of the `WORKFILE` variable is `/home/jim/program.c`, then this command displays `program.c`.

2. To construct a filename that is the same as another filename (except for the suffix), enter:

```shell
OFILE=`basename $1 .c`.o
```

This command assigns the value of the first positional parameter ($1) to the `OFILE` file, but changes its `.c` suffix to `.o`. If `$1` is `/home/jim/program.c`, then `OFILE` becomes `program.o`. Since `program.o` is only a base filename, it identifies a file in the current directory.
