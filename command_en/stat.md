stat
===

Displays file or file system status

## Description

The **stat command** is used to display status information about files. The output of the `stat` command is more detailed than that of the `ls` command.

### Syntax

```shell
stat (options) (parameters)
```

### Options

```shell
-L: Support symbolic links;
-f: Display file system status instead of file status;
-t: Output information in a concise format;
--help: Display help information for the command;
--version: Display version information for the command.
```

### Parameters

File: Specify the regular file or device file corresponding to the file system to display information for.

### Examples

```shell
[root@localhost ~]# ls -l myfile
-rw-r--r-- 1 root root 0 2010-10-09 myfile

[root@localhost ~]# stat myfile
file: “myfile”
Size: 0               Blocks: 8          IO Block: 4096   Regular empty file
Device: fd00h/64768d    Inode: 194805815   Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2010-12-12 12:22:35.000000000 +0800
Modify: 2010-10-09 20:44:21.000000000 +0800
Change: 2010-10-09 20:44:21.000000000 +0800

[root@localhost ~]# stat -f myfile
File: "myfile"
id: 0        Namelen: 255     type: ext2/ext3
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 241555461  free: 232910771  Available: 220442547
Inodes: Total: 249364480  Free: 249139691

[root@localhost ~]# stat -t myfile
myfile 0 8 81a4 0 0 fd00 194805815 1 0 0 1292127755 1286628261 1286628261 4096
```
