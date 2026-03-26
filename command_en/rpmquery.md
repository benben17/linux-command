rpmquery
===

Query package information from the RPM database.

## Description

The **rpmquery command** queries package information from the RPM database based on various criteria.

### Syntax

```shell
rpmquery(options)
```

### Options

```shell
-qf: Query the package that a specified file belongs to.
-q: Query whether a specified package is installed.
-qc: Query configuration files in a package.
-qd: Query documentation files in a package.
-qi: Query basic information about a package.
```

### Examples

Use the `rpmquery` command to query the package that a specified file belongs to:

```shell
[root@localhost ~]# rpmquery -qf /usr/bin/htpasswd
httpd-2.2.3-81.el5.centos
```
