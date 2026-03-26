dpkg
===

Install, build, and manage Debian packages.

## Description

The **dpkg** command is a utility tool used in Debian Linux systems to install, build, and manage software packages.

### Syntax

```shell
dpkg (options) (parameters)
```

### Options

```shell
-i    Install the package.
-r    Remove the package.
-P    Purge the package (remove the package and its configuration files).
-L    List files associated with the package.
-l    List installed packages.
--unpack  Unpack the package but do not configure it.
-c    List the contents of a .deb package.
--configure  Configure a package that has been unpacked but not yet configured.
```

### Parameters

Deb Package: Specifies the .deb package to operate on.

### Examples

```shell
dpkg -i package.deb     # Install package
dpkg -r package         # Remove package
dpkg -P package         # Purge package (including configuration files)
dpkg -L package         # List files associated with the package
dpkg -l package         # Show version of the package
dpkg --unpack package.deb  # Unpack the contents of a deb package
dpkg -S keyword            # Search for a package containing the keyword
dpkg -l                    # List all currently installed packages
dpkg -c package.deb        # List contents of a deb package
dpkg --configure package   # Configure the package
```
