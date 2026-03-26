whereis
===

Locate the binary, source, and manual page files for a command

## Description

The **whereis command** is used to locate the binary, source, and manual page files for specified commands.

The `whereis` command only searches for programs and restricts its search to binary files (option `-b`), manual pages (option `-m`), and source code files (option `-s`). If no options are provided, all information is returned.

Compared to `find`, `whereis` is much faster because it searches a database containing information about all files in the system, rather than traversing the hard drive. However, this database is not updated in real-time (typically once a week), so `whereis` might return paths for deleted files or fail to find newly created ones.

### Syntax

```shell
whereis [options] [command_name]
```

### Options

```shell
-b  Search only for binaries.
-B <directory>  Limit the search for binaries to the specified directory.
-f  Terminate the directory list and signal the start of filenames.
-m  Search only for manual pages.
-M <directory>  Limit the search for manual pages to the specified directory.
-s  Search only for source files.
-S <directory>  Limit the search for source files to the specified directory.
-u  Search for unusual entries (commands that don't have exactly one entry of each requested type).
```

### Parameters

command_name: The name of the command to locate.

### Examples

Find all related files:

```shell
[root@localhost ~]# whereis tomcat
tomcat:

[root@localhost ~]# whereis svn
svn: /usr/bin/svn /usr/local/svn /usr/share/man/man1/svn.1.gz
```

Locate only binaries:

```shell
[root@localhost ~]# whereis -b svn
svn: /usr/bin/svn /usr/local/svn
```

Locate only manual pages:

```shell
[root@localhost ~]# whereis -m svn
svn: /usr/share/man/man1/svn.1.gz
```

Locate only source files:

```shell
[root@localhost ~]# whereis -s svn
svn:
```
