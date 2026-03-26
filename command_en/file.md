file
===

Used to determine the type of a given file.

## Description

The **file command** is used to detect the type of a given file. It examines files through three sets of tests: filesystem tests, magic number tests, and language tests.

### Syntax

```shell
file (options) (parameters)
```

### Options

```shell
-b: Do not prepend filenames to output lines (brief mode).
-c: Display the detailed execution process of the command, useful for debugging or analyzing how files are being identified.
-f <namefile>: Read the names of the files to be examined from <namefile> (one per line) before identifying them.
-L: Follow symbolic links and identify the type of the file the link points to.
-m <magicfile>: Specify an alternate magic number file.
-v: Display version information.
-z: Attempt to look inside compressed files.
```

### Parameters

File: A list of files to be typed, separated by spaces. Shell wildcards can be used to match multiple files.

### Examples

Display file type:

```shell
[root@localhost ~]# file install.log
install.log: UTF-8 Unicode text

[root@localhost ~]# file -b install.log      <== Do not display the filename
UTF-8 Unicode text

[root@localhost ~]# file -i install.log      <== Display MIME type.
install.log: text/plain; charset=utf-8

[root@localhost ~]# file -b -i install.log
text/plain; charset=utf-8
```

Display the file type of a symbolic link:

```shell
[root@localhost ~]# ls -l /var/mail
lrwxrwxrwx 1 root root 10 08-13 00:11 /var/mail -> spool/mail

[root@localhost ~]# file /var/mail
/var/mail: symbolic link to `spool/mail'

[root@localhost ~]# file -L /var/mail
/var/mail: directory

[root@localhost ~]# file /var/spool/mail
/var/spool/mail: directory

[root@localhost ~]# file -L /var/spool/mail
/var/spool/mail: directory
```
