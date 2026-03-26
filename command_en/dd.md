dd
===

Convert and copy a file

## Supplemental Information

The **dd command** is used to copy a file while performing conversions and formatting on the original content. It is a powerful tool often used for low-level operations where other commands might not suffice. A common use case is backing up raw devices, though for specific applications like databases, specialized tools are generally preferred for better manageability.

It is recommended to use `dd` for physical disk operations. For file system tasks, commands like `tar` or `cpio` are often more convenient. When using `dd` for disk operations, it is best to use block device files.

### Syntax

```shell
dd (options)
```

### Options

```shell
bs=<bytes>: Set both input (ibs) and output (obs) block size to the specified number of bytes;
cbs=<bytes>: Convert the specified number of bytes at a time;
conv=<keywords>: Specify how the file should be converted (comma-separated list);
count=<blocks>: Copy only the specified number of input blocks;
ibs=<bytes>: Read the specified number of bytes at a time;
obs=<bytes>: Write the specified number of bytes at a time;
if=<file>: Read from the specified file instead of stdin;
of=<file>: Write to the specified file instead of stdout;
seek=<blocks>: Skip the specified number of blocks at the start of the output;
skip=<blocks>: Skip the specified number of blocks at the start of the input;
--help: Display help;
--version: Display version information.
```

### Examples

```shell
[root@localhost text]# dd if=/dev/zero of=sun.txt bs=1M count=1
1+0 records in
1+0 records out
1048576 bytes (1.0 MB) copied, 0.006107 seconds, 172 MB/s

[root@localhost text]# du -sh sun.txt 
1.1M    sun.txt
```

This command creates a 1MB file named `sun.txt`. Parameter explanation:

* **if**: Input file. Defaults to stdin if not specified.
* **of**: Output file. Defaults to stdout if not specified.
* **bs**: Block size in bytes.
* **count**: Number of blocks to copy.
* **/dev/zero**: A character device that provides as many null bytes (\0) as requested.

Block size units:

Unit | Code
---- | ----
Byte (1B) | c
Word (2B) | w
Block (512B) | b
Kilobyte (1024B) | k
Megabyte (1024KB) | M
Gigabyte (1024MB) | G

The output also shows the performance of the operation:

```shell
1048576 bytes (1.0 MB) copied, 0.006107 seconds, 172 MB/s
```

**Generating a Random String**

You can use `/dev/urandom` with `dd` to generate random strings:

```shell
[root@localhost ~]# dd if=/dev/urandom bs=1 count=15 | base64 -w 0
15+0 records in
15+0 records out
15 bytes (15 B) copied, 0.000111993 s, 134 kB/s
wFRAnlkXeBXmWs1MyGEs
```

**Testing Disk Write Speed**

```shell
[root@localhost ~]# dd if=/dev/zero of=/tmp/testfile bs=1G count=1 oflag=direct
1+0 records in
1+0 records out
1073741824 bytes (1.1 GB) copied, 7.10845 s, 151 MB/s
```

**Testing Disk Read Speed**

```shell
[root@localhost ~]# dd if=/tmp/testfile of=/dev/null bs=1G count=1 iflag=direct
1+0 records in
1+0 records out
1073741824 bytes (1.1 GB) copied, 6.53009 s, 164 MB/s
```
