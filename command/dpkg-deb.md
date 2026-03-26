dpkg-deb
===

Debian package archive (.deb) manipulation tool.

## Description

The **dpkg-deb** command is a package management tool for Debian Linux. It can pack and unpack software packages and provide information about them.

### Syntax

```shell
dpkg-deb (options) (parameters)
```

### Options

```shell
-c    List the contents of an archive.
-e    Extract control information from an archive.
-f    Print the value of the control file field(s).
-x    Extract the files contained in an archive to a specified directory.
-X    Extract the files contained in an archive to a specified directory and list them as they are extracted.
-w    Display information about an archive.
-l    Display detailed information about an archive.
-R    Extract control information and the contents of an archive.
-b    Build a Debian archive.
```

### Parameters

File: Specifies the full name or software name of the ".deb" package to operate on.

### Examples

Extract program files:

```shell
dpkg-deb -x drcom-pum_1.0-0ubuntu1~ppa1~jaunty1_i386.deb drcom
```

Extract control files:

```shell
dpkg-deb -e drcom-pum_1.0-0ubuntu1~ppa1~jaunty1_i386.deb drcom/DEBIAN
```

Build a .deb file:

```shell
dpkg-deb -b drcom drcom_1.4.8.2_i386.deb
```

Query the contents of a .deb package:

```shell
dpkg-deb -c demo.deb
```
