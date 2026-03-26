mkdir
===

Create directories

## Description

The **mkdir command** is used to create one or more directories. If no path is provided, the directory is created in the current working directory. If an existing path is specified, the directory is created within that path. When creating a directory, ensure that its name does not conflict with existing files or directories in the same location.

Organizing files into subdirectories (e.g., by type or purpose) is a best practice for effective file management.

### Syntax

```shell
mkdir [OPTION]... DIRECTORY...
```

### Options

```shell
-Z: Set the SELinux security context.
-m, --mode <MODE>: Set the file mode (permissions) for the new directory.
-p, --parents: Create parent directories as needed. No error if they already exist.
--version: Display version information.
```

### Parameters

Directory: A space-separated list of directories to be created.

### Examples

Create a subdirectory named `test` in `/usr/meng` with permissions set to 700 (read, write, and execute for the owner only):

```shell
mkdir -m 700 /usr/meng/test
```

Create a directory `bin` and its subdirectory `os_1` in the current directory, with permissions set to 750 (owner: rwx, group: r-x, others: none):

```shell
mkdir -p -m 750 bin/os_1
```

### Permissions Reference

The `-m` option configures directory permissions using a three-digit numeric code:

-   **First digit**: Owner's (user) permissions.
-   **Second digit**: Group's permissions.
-   **Third digit**: Others' permissions.

Each digit is a sum of:
-   4: Read (r)
-   2: Write (w)
-   1: Execute (x)

For example, `755` corresponds to:
-   `7` (Owner) = 4 + 2 + 1 = `rwx`
-   `5` (Group) = 4 + 1 = `r-x`
-   `5` (Others) = 4 + 1 = `r-x`
