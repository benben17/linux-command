md5sum
===

Compute and check MD5 message digests

## Description

The **md5sum command** uses the MD5 message-digest algorithm (128-bit) to calculate and verify file checksums. It is a standard tool included with most Linux distributions.

MD5 is frequently used to verify the integrity of files transferred over a network, ensuring that they have not been corrupted or tampered with. The algorithm processes any length of information bit by bit to produce a 128-bit (32 hexadecimal characters) "fingerprint" or "digest". It is highly unlikely for two different files to produce the same digest.

### Syntax

```shell
md5sum [OPTION]... [FILE]...
```

### Options

```shell
-b, --binary   Read in binary mode.
-t, --text     Read in text mode (default).
-c, --check    Read MD5 sums from the FILEs and check them.
--status       Don't output anything, status code shows success.
-w, --warn     Warn about improperly formatted checksum lines.
```

### Parameters

File: The path to the file(s) to be processed. When using `-c`, this is the file containing the checksums.

### Examples

**Generating a Random String using md5sum**

A common trick to generate a random string (useful for passwords) is to compute the MD5 hash of a dynamic input like the current date:

```shell
[root@localhost ~]# date | md5sum
6a43f2c246cdc3e6a3592652f831d186  -
```

**Generate the MD5 checksum for a file:**

```shell
[root@localhost ~]# md5sum insert.sql
bcda6cb5c704664f989703ac5a88f112  insert.sql
```

**Check if a file has been modified:**

First, generate the MD5 checksum file:

```shell
md5sum testfile > testfile.md5
```

Then, verify the file using the checksum:

```shell
md5sum -c testfile.md5
```

If the file is unchanged, the output will be:

```shell
testfile: OK
```

The command returns an exit status of 0.

If the file has been modified, the output will be:

```shell
testfile: FAILED
md5sum: WARNING: 1 of 1 computed checksum did NOT match
```

The command returns a non-zero exit status.

To perform a check silently, use the `--status` option and verify the return value:

```shell
md5sum --status -c testfile.md5
```
