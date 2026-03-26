bunzip2
===

Decompress files in .bz2 format.

## Description

`bzip2` can compress and decompress files. This command is similar to the `gzip/gunzip` commands and can only compress files. For directories, it can only compress all files within the directory. Once compressed, a package with the `.bz2` suffix is generated in the directory. **bunzip2 is actually a symbolic link to bzip2**, meaning it is a soft link; therefore, decompression can always be achieved via `bzip2 -d`.

### Syntax

```shell
bunzip2 [options] [parameters]
```

### Options

```shell
-f or --force: Force overwrite of existing files with the same name during decompression.
-k or --keep: By default, the original compressed file is deleted after decompression. Use this parameter to keep the compressed file.
-s or --small: Reduce memory usage during program execution.
-v or --verbose: Show detailed information during file decompression.
-l, --license, -V or --version: Display version information.
```

### Parameters

.bz2 compressed package: Specify the `.bz2` package that needs to be decompressed.

### Examples

Compress `etc.zip`, `var.zip`, and `backup.zip` in the `/opt` directory, set the compression rate to maximum, do not delete original files after compression, and show detailed information about the compression process.

```shell
bzip2 -9vk /opt/etc.zip /opt/var.zip /opt/backup.zip
```

After compression, corresponding `etc.zip.bz2`, `var.zip.bz2`, and `backup.zip.bz2` files will be generated in `/opt`.

Decompress:

```bash
bunzip2 -v /opt/etc.zip.bz2
```
