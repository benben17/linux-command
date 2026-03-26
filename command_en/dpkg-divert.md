dpkg-divert
===

Override a package's version of a file in Debian.

## Description

The **dpkg-divert** command is a utility in Debian Linux used to create and manage a list of diversions. Diversions allow you to move a file from its default location, preventing it from being overwritten when a package is installed.

### Syntax

```shell
dpkg-divert (options) (parameters)
```

### Options

```shell
--add       Add a diversion.
--remove    Remove a diversion.
--list      List diversions matching a pattern.
--truename  Display the real name for a diverted file.
--quiet     Quiet mode, minimize output.
```

### Parameters

File: Specifies the file name for the diversion.

### Examples

Specify that when the package `wibble` is installed, it should write to `/usr/bin/example.foo` instead of `/usr/bin/example`:

```shell
dpkg-divert --package wibble --divert /usr/bin/example.foo --rename /usr/bin/example
```

Remove the diversion for `/usr/bin/example` associated with the package `wibble`:

```shell
dpkg-divert --package wibble --rename --remove /usr/bin/example
```

Remove any diversion for `/usr/bin/example`:

```shell
dpkg-divert --rename --remove /usr/bin/example
```

Add a diversion so that any package trying to install to `/usr/bin/example` will write to `/usr/bin/example.foo` instead:

```shell
dpkg-divert --divert /usr/bin/example.foo --rename /usr/bin/example
```
