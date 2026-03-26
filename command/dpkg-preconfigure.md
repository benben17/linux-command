dpkg-preconfigure
===

Pre-configure Debian packages before they are installed.

## Description

The **dpkg-preconfigure** command is used in Debian Linux to ask configuration questions before a package is actually installed.

### Syntax

```shell
dpkg-preconfigure (options) (parameters)
```

### Options

```shell
-f       Select the frontend to use.
-p       Specify the minimum priority of questions to ask.
--apt    Run in APT mode.
```

### Parameters

Package: Specifies the ".deb" package file(s).

### Examples

Import debconf templates:

```shell
dpkg-preconfigure /var/cache/apt/archives/mysql-server-5.5*.deb
```
