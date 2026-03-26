pigz
===

Parallel implementation of gzip for faster compression and decompression.

## Description

The **pigz command** (Parallel Implementation of GZip) is a fully functional replacement for gzip that exploits multiple processors and multiple cores when compressing data. It is significantly faster than gzip.

Homepage: [http://zlib.net/pigz/](http://zlib.net/pigz/)

### Syntax

```shell
pigz [ -cdfhikKlLmMnNqrRtz0..9,11 ] [ -b blocksize ] [ -p threads ] [ -S suffix ] [ name ...  ]
unpigz [ -cfhikKlLmMnNqrRtz ] [ -b blocksize ] [ -p threads ] [ -S suffix ] [ name ...  ]
```

### Options

```shell
-0 to -9, -11       # Compression level (level 11, using zopfli, is much slower).
--fast, --best      # Shorthand for compression levels 1 and 9 respectively.
-b, --blocksize mmm # Set compression block size to mmmK (default 128K).
-c, --stdout        # Write output to standard output (don't delete original files).
-d, --decompress    # Decompress the input.
-f, --force         # Force overwrite of output file.
-h, --help          # Display help information.
-i, --independent   # Compress blocks independently for better damage recovery.
-k, --keep          # Do not delete the original file after processing.
-K, --zip           # Compress to PKWare zip (.zip) format.
-l, --list          # List the contents of the compressed input.
-p, --processes n   # Use n threads (default is the number of online processors).
-q, --quiet         # Suppress all warnings and messages.
-r, --recursive     # Process subdirectories recursively.
-S, --suffix .sss   # Use a custom suffix instead of .gz.
-t, --test          # Test the integrity of the compressed file.
-v, --verbose       # Provide detailed progress information.
-V, --version       # Show the version of pigz.
-z, --zlib          # Compress to zlib (.zz) format instead of gzip.
```

### Examples

**Compress multiple directories using tar and pigz:**

```shell
tar -cvf - dir1 dir2 dir3 | pigz -p 8 > output.tgz
```

**Decompress using pigz:**

```shell
pigz -p 8 -d output.tgz
```

**Decompress a pigz-compressed file using tar:**

```shell
tar -xzvf output.tgz
```
