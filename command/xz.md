xz
===

High compression ratio utility for POSIX platforms.

## Supplemental Information

**xz** is part of XZ Utils, a set of free lossless data compression software for POSIX-like operating systems. It uses the LZMA2 compression algorithm, producing smaller compressed files than traditional gzip or bzip2 while maintaining fast decompression speeds. Initially based on the LZMA-SDK, XZ Utils was heavily modified to better suit POSIX platforms and eventually replace the older LZMA Utils.

### Syntax

```shell
xz (options) (parameters)
xz [OPTION]... [FILE]...
```

### Options

```shell
-z, --compress    # Force compression
-d, --decompress, --uncompress
                  # Force decompression
-t, --test        # Test the integrity of compressed files
-l, --list        # List information about .xz files
-k, --keep        # Keep (do not delete) input files
-f, --force       # Force overwrite of output files and (de)compress links
-c, --stdout, --to-stdout
                  # Write to standard output, do not delete input files
-0 ... -9         # Compression presets; default is 6
                  # Consider memory usage for decompression before using 7-9!
-e, --extreme     # Try to improve compression ratio by using more CPU time;
                  # Does not affect decompression memory requirements
-T, --threads=NUM # Use at most NUM threads; default is 1;
                  # Set to 0 to use as many threads as there are processor cores
-q, --quiet       # Suppress warnings; specify twice to suppress errors
-v, --verbose     # Verbose; specify twice for even more detail
-h, --help        # Display summary help and exit
-H, --long-help   # Display long help (includes advanced options)
-V, --version     # Display version information and exit
```

### Parameters

* Source file: The file to be compressed or decompressed.
* Target file: The resulting file after the operation.

### Examples

Compress a file `test.txt`. Upon success, `test.txt.xz` is created and the original file is deleted.

```shell
$ xz test.txt
$ ls test.txt*

test.txt.xz
```

Decompress `test.txt.xz` and use the `-k` option to keep the original compressed file.

```shell
$ xz -d -k test.txt.xz
$ ls test.txt*

test.txt.xz test.txt
```

Use the `-l` option to display basic information about a `.xz` file, including compression ratio and integrity check method. Can be combined with `-v` or `-vv` for more details.

```shell
xz -l index.txt.xz
# Strms  Blocks   Compressed Uncompressed  Ratio  Check   Filename
#    1       1        768 B      1,240 B  0.619  CRC64   index.txt.
```

Set the compression level using `-0`, `-1`, ... `-9` or `--fast`, `--best`. The default for `xz` is `-6`, which offers a good balance for most systems.

```shell
$ xz -k7 xz_pipe_decomp_mini.c
$ xz -k --fast xz_pipe_decomp_mini.c
```

Use `-H` to display all `xz` options in detail (more comprehensive than `--help`).

```shell
$ xz -H | more
```

Compress multiple files in parallel using `xargs`. The following command compresses all `.log` files in `/var/log` by running multiple `xz` processes simultaneously.

```shell
# Root privileges required.
find /var/log -type f -iname "*.log" -print0 | xargs -P4 -n16 xz -T1
```
