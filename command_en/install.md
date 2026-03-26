install
===

Copy files and set attributes.

## Description

The `install` command is used to copy files or directories while allowing you to control the attributes of the destination files. It is similar to `cp` but is primarily used in makefiles to install programs into target directories.

### Syntax

```shell
install [OPTION]... [-T] SOURCE DEST
install [OPTION]... SOURCE... DIRECTORY
install [OPTION]... -t DIRECTORY SOURCE...
install [OPTION]... -d DIRECTORY...
```

The first two formats copy source files to a destination or an existing directory while setting permissions and ownership. The third format creates all specified directories and their parent directories.

### Options

```shell
--backup[=CONTROL] : Back up each existing destination file.
-b : Like --backup but accepts no arguments.
-d, --directory : Treat all arguments as directory names and create them (including parents).
-D : Create all leading components of DEST, then copy SOURCE to DEST.
-g, --group=GROUP : Set group ownership.
-m, --mode=MODE : Set permission mode (like chmod) instead of rwxr-xr-x.
-o, --owner=OWNER : Set ownership (root only).
-p, --preserve-timestamps : Preserve source access/modification times.
-s, --strip : Strip symbol tables (for binaries).
-S, --suffix=SUFFIX : Override the usual backup suffix.
-v, --verbose : Print the name of each directory or file as it is processed.
--help : Display help and exit.
--version : Output version information and exit.
```

### Examples

**Create directories (recursive like `mkdir -p`):**

```shell
install -d a/b/c e/f
```

**Copy a file to a destination file:**

```shell
install source_file dest_file
```

**Using the `-D` option to create parent directories on the fly:**

```shell
install -D x a/b/c
# Equivalent to: mkdir -p a/b && cp x a/b/c
```

**Copy multiple files to a directory:**

```shell
install source_files/* target_directory/
```
