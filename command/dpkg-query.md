dpkg-query
===

A tool to query the dpkg database.

## Description

The **dpkg-query** command is a tool for querying information about packages from the `dpkg` package database.

### Syntax

```shell
dpkg-query (options) (parameters)
```

### Options

```shell
-l    List packages matching the given pattern.
-s    Report status of the specified package.
-L    List files installed to your system from the specified package.
-S    Search for a file name in installed packages.
-w    Display information about the specified package(s).
-c    Display the path to the package's control file.
-p    Display details about the specified package.
```

### Parameters

Package Name: Specifies the package to query.

### Examples

Find which package installed a specific file (`file1`):

```shell
dpkg-query -S file1
```

List installed packages and their versions on Ubuntu:

```shell
dpkg-query -W --showformat='${Package} ${Version}\n' > filename
```

View detailed information about a package (`capistrano`):

```shell
dpkg-query -s capistrano
```

List files installed by a specific package:

```shell
dpkg-query -L capistrano
```

List all installed packages:

```shell
dpkg-query -l
```

Check the exact status (e.g., whether it is installed) and version of a package:

```shell
dpkg-query -W -f='${Status} ${Version}\n' apache-perl
```
