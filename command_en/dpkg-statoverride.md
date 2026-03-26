dpkg-statoverride
===

Override ownership and mode of files in Debian.

## Description

The **dpkg-statoverride** command is used in Debian Linux to override the ownership and mode of files. It tells `dpkg` to use a different owner or mode for a path when a package is installed.

### Syntax

```shell
dpkg-statoverride (options)
```

### Options

```shell
--add       Add a new override.
--remove    Remove an override.
--list      List all current overrides.
--update    Immediately update the file's ownership and mode if the file exists.
```

### Examples

Change the permission attributes of a folder:

```shell
sudo dpkg-statoverride --update --add nagios nagios 751 /var/lib/nagios3
```

Force change the permission attributes of a folder:

```shell
sudo dpkg-statoverride --force --update --add root sasl 755 /var/spool/postfix/var/run/saslauthd
```

Remove a file's override from the database:

```shell
sudo dpkg-statoverride --remove /usr/bin/wall
```
