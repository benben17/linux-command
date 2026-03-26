gzip
===

Compress files.

## Supplemental Information

The **gzip command** is used to compress files. It is a widely used compression utility; after a file is compressed, it will have a `.gz` extension added to its name.

`gzip` is a frequently used command in Linux for both compressing and decompressing files, known for being convenient and efficient. It is not only used to compress large or infrequently used files to save disk space but is also commonly used in conjunction with the `tar` command to create the popular compressed archive formats. Statistics show that `gzip` can achieve a 60%–70% compression ratio for text files. Reducing file size provides two main benefits: saving storage space and reducing the time required for network transfers.

### Syntax

```shell
gzip (options) (parameters)
```

### Options

```shell
-a, --ascii: Use ASCII text mode;
-d, --decompress, --uncompress: Decompress the compressed file;
-f, --force: Force compression even if files already exist or are hard links or symbolic links;
-h, --help: Display online help;
-l, --list: List information about the compressed file;
-L, --license: Display version and copyright information;
-n, --no-name: When compressing, do not save the original file name and time stamp;
-N, --name: When compressing, save the original file name and time stamp;
-q, --quiet: Suppress all warnings;
-r, --recursive: Recursively process all files and subdirectories in the specified directory;
-S <suffix>, --suffix <suffix>: Use <suffix> as the compression suffix;
-t, --test: Test the integrity of the compressed file;
-v, --verbose: Display verbose output;
-V, --version: Display version information;
-<num>: Set the compression level to <num>, where <num> is between 1 and 9. The default is 6. A higher value provides better compression but takes longer;
--best: Same as -9;
--fast: Same as -1;
-c, --stdout, --to-stdout: Keep original files and write output to standard output (often used with redirection).
```

### Parameters

File List: Specifies the list of files to be compressed.

### Examples

Compress every file in the `test6` directory into `.gz` files:

```shell
gzip *
```

Decompress each compressed file from the previous example and list detailed information:

```shell
gzip -dv *
```

Show detailed information for each compressed file from Example 1 without decompressing:

```shell
gzip -l *
```

Compress a tar archive, resulting in a `.tar.gz` file:

```shell
gzip -r log.tar
```

Recursively compress a directory:

```shell
gzip -rv test6
```

In this case, all files inside `test6` are turned into `.gz` files. The directory structure remains, but the files within are replaced by their compressed versions. This is compression, not archiving. Because it operates on a directory, the `-r` option is required for recursion.

Recursively decompress a directory:

```shell
gzip -dr test6
```

Keep original files and redirect the compression/decompression stream to a new file:

```shell
gzip -c aa > aa.gz
gzip -dc bb.gz > bb
```
