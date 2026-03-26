gunzip
===

Decompress files.

## Supplemental Information

The **gunzip command** is a widely used utility for decompressing files. It is primarily used to decompress files compressed with `gzip`, which typically have a `.gz` extension. In fact, `gunzip` is a hard link to `gzip`, meaning both compression and decompression can be performed using the `gzip` command alone.

### Syntax

```shell
gunzip (options) (parameters)
```

### Options

```shell
-a, --ascii: Use ASCII text mode;
-c, --stdout, --to-stdout: Output the decompressed data to standard output;
-f, --force: Force decompression even if files already exist or are symbolic links;
-h, --help: Display online help;
-l, --list: List information about the compressed files;
-L, --license: Display version and copyright information;
-n, --no-name: When decompressing, ignore any original file name and time stamp;
-N, --name: When decompressing, restore the original file name and time stamp;
-q, --quiet: Suppress all warnings;
-r, --recursive: Decompress all files in the specified directory and its subdirectories;
-S <suffix>, --suffix <suffix>: Use <suffix> as the compression suffix;
-t, --test: Test the integrity of the compressed file;
-v, --verbose: Display verbose output;
-V, --version: Display version information;
```

### Parameters

File List: Specifies the compressed files to be decompressed.

### Examples

First, compress all files and subdirectories in `/etc`, backup the archive to `/opt/etc.zip`, and then compress `etc.zip` using `gzip` with a compression level of 9.

```shell
zip -r /opt/etc.zip /etc
gzip -9v /opt/etc.zip
```

View the compression information of the resulting `etc.zip.gz` file.

```shell
gzip -l /opt/etc.zip.gz
compressed        uncompressed ratio uncompressed_name
11938745            12767265   6.5% /opt/etc.zip
```

Decompress the `etc.zip.gz` file into the current directory.

```shell
gunzip /opt/etc.zip.gz
# or
gzip -d /opt/etc.zip.gz
```

As shown in the example, `gzip -d` is equivalent to the `gunzip` command.
