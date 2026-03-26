compress
===

Compress data files using Lempel-Ziv encoding

## Description

The **compress command** uses "Lempel-Ziv" encoding to compress data files. `compress` is a historical compression program; files compressed by it will have a ".Z" extension. To decompress, you can use the `uncompress` command. In fact, `uncompress` is a symbolic link to `compress`, so both compression and decompression can be performed using the `compress` command.

### Syntax

```shell
compress [options] [arguments]
```

### Options

```shell
-f: Force overwrite of the target file without prompting the user.
-c: Write the result to standard output; no files are changed.
-r: Recursive operation.
-b <bits>: Compression efficiency, a value between 9 and 16 (default is 16). Higher values result in better compression.
-d: Decompress the file instead of compressing it.
-v: Display the progress of the command.
-V: Display the version and program defaults.
```

### Arguments

Files: Specify the list of files to be compressed.

### Examples

Copy `/etc/man.config` to `/tmp` and compress it:

```shell
[root@localhost ~]# cd /tmp
[root@localhost tmp]# cp /etc/man.config .
[root@localhost tmp]# compress man.config
[root@localhost tmp]# ls -l
```

```shell
-rw-r--r-- 1 root root 2605 Jul 27 11:43 man.config.Z
```

Decompress the file:

```shell
[root@localhost tmp]# compress -d man.config.Z
```

Compress `man.config` into a different file as a backup:

```shell
[root@localhost tmp]# compress -c man.config > man.config.back.Z
[root@localhost tmp]# ll man.config*
```

```shell
-rw-r--r-- 1 root root 4506 Jul 27 11:43 man.config
-rw-r--r-- 1 root root 2605 Jul 27 11:46 man.config.back.Z
```

The `-c` option is useful as it sends the compressed data to standard output instead of creating a `.Z` file directly, allowing you to redirect it to a different filename.
