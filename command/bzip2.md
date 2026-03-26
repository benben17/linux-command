bzip2
===

A block-sorting file compressor.

## Description

The **bzip2 command** is used to create and manage (including decompressing) compressed packages in `.bz2` format.

`bzip2` compresses files using the Burrows-Wheeler block sorting text compression algorithm and Huffman coding. Compression rates are generally considerably better than those achieved by LZ77/LZ78-based compressors, and approach the performance of the PPM family of statistical compressors.

The command-line arguments are deliberately designed to be very similar to those of GNU `gzip`, but they are not identical.

`bzip2` expects a list of file names to accompany the command-line flags. Each file is replaced by a compressed version of itself, with the name `original_name.bz2`. Each compressed file has the same modification date, permissions, and, when possible, ownership as the corresponding original, so that these properties can be correctly restored at decompression time. On some file systems, there is no concept of permissions, ownership, or dates, or there are strict limits on the length of file names (such as MSDOS). In these cases, `bzip2` has no mechanism to maintain original file names, owners, permissions, and times; in this sense, `bzip2`'s handling of file names is naive.

`bzip2` and `bunzip2` will by default not overwrite existing files. If you want to overwrite existing files, specify the `-f` flag.

If no file names are specified, `bzip2` compresses from standard input to standard output. In this case, `bzip2` will decline to write compressed output to a terminal, as this would be entirely incomprehensible and therefore pointless.

`bunzip2` (or `bzip2 -d`) decompresses all specified files. Files that were not created by `bzip2` will be ignored, and a warning will be issued. `bzip2` determines the decompressed file name from the compressed file name as follows:

```shell
filename.bz2    becomes   filename
filename.bz     becomes   filename
filename.tbz2   becomes   filename.tar
filename.tbz    becomes   filename.tar
anyothername    becomes   anyothername.out
```

If the file does not have one of the recognized extensions (.bz2, .bz, .tbz2, or .tbz), `bzip2` complains that it cannot guess the name of the original file, and uses the original name with `.out` appended.

When compressing, if no filename is provided, `bzip2` reads from standard input and writes the compressed result to standard output.

`bzip2` uses a 32-bit CRC for self-checking to ensure that the decompressed file is identical to the original. This can be used to detect corruption in the compressed file and to guard against unknown bugs in `bzip2` (this is very unlikely, with luck). The chance of data corruption going undetected is microscopic, about one in four billion for each file processed. The check is performed at decompression time, so it can only indicate that something is wrong. It can help recover the original uncompressed data. You can use `bzip2recover` to try to recover data from damaged files.

Return values: 0 for a normal exit, 1 for environmental problems (file not found, invalid flags, I/O errors, etc.), 2 to indicate a corrupt compressed file, and 3 for an internal consistency error (e.g., a bug) that causes `bzip2` to panic.

### Syntax

```shell
bzip2 [ -cdfkqstvzVL123456789 ] [ filenames ... ]
```

### Options

```shell
-c --stdout
    # Compress or decompress to standard output.

-d --decompress
    # Force decompression. bzip2, bunzip2, and bzcat are actually the same program; the action taken is determined by the program name. This flag overrides that mechanism and forces bzip2 to decompress.

-z --compress
    # Complement to -d: forces compression, regardless of the invocation name.

-t --test
    # Check integrity of the specified file(s), but don't decompress them. This effectively performs a trial decompression and throws away the result.

-f --force
    # Force overwrite of output files. Normally, bzip2 will not overwrite existing output files. It also forces bzip2 to break hard links to files, which it otherwise wouldn't do.

-k --keep
    # Keep (don't delete) input files during compression or decompression.

-s --small
    # Reduce memory usage for compression, decompression, and testing. Files are decompressed and tested using a modified algorithm which only requires 2.5 bytes per block byte. This means any file can be decompressed in 2300k of memory, albeit at about half the normal speed.

    # When compressing, -s selects a block size of 200k, which limits memory usage to around the same figure, at the expense of compression ratio. In short, if your machine is low on memory (8 megabytes or less), you might want to use -s for everything. See MEMORY MANAGEMENT below.

-q --quiet
    # Suppress non-essential warning messages. Messages which pertain to I/O errors and other critical events will not be suppressed.

-v --verbose
    # Verbose mode -- show the compression ratio for each file processed. Further -v's increase the verbosity level, spewing out lots of information which is primarily of interest for diagnostic purposes.

-L --license -V --version
    # Display the software version, license terms and conditions.

-1 to -9
    # Set the block size to 100 k, 200 k ... 900 k when compressing. Has no effect when decompressing. See MEMORY MANAGEMENT below.

-- # Treats all subsequent arguments as file names, even if they start with a dash. This allows handling files with names starting with a dash, e.g., bzip2 -- -myfilename.

--repetitive-fast --repetitive-best
    # These flags are redundant in versions 0.9.5 and above. They provided some coarse control over the behavior of the sorting algorithm in earlier versions, which was sometimes useful. 0.9.5 and above use an improved algorithm which renders these flags irrelevant.
```

### Parameters

File: Specify the file(s) to be compressed.

### Examples

**Compress a specific file (e.g., filename):**

```shell
bzip2 filename
# or
bzip2 -z filename
```

Here, there is no output during compression; the original `filename` is deleted and replaced by `filename.bz2`. If `filename.bz2` already exists, it will not be replaced and an error will be displayed (to replace it, use the `-f` flag, e.g., `bzip2 -f filename`). If `filename` is a directory, an error is also prompted and no action is taken. If `filename` is already compressed with a `.bz2` suffix, a warning is given and it won't be re-compressed; if it doesn't have the suffix, it will be compressed again.

**Decompress a specific file (e.g., filename.bz2):**

```shell
bzip2 -d filename.bz2
# or
bunzip2 filename.bz2
```

Here, there is no standard output during decompression; the original `filename.bz2` is replaced by `filename`. If `filename` already exists, it will not be replaced and an error will be displayed (to replace it, use the `-f` flag, e.g., `bzip2 -df filename.bz2`).

**Show output during compression/decompression:**

```shell
$ bzip2 -v filename
```

Output:

```shell
filename:  0.119:1, 67.200 bits/byte, -740.00% saved, 5 in, 42 out.
```

Here, adding the `-v` flag provides output. Decompression works similarly: `bzip2 -dv filename.bz2`.

**Test decompression without actually decompressing:**

```shell
bzip2 -tv filename.bz2
```

Output:

```shell
filename.bz2: ok
```

Here, `-t` specifies a trial decompression without producing output files, effectively checking the file. Even if `filename` exists in the directory, no error will be reported because it's not actually decompressing. The `-v` flag is added to see the output on the screen; for actual decompression, `bzip2 -dv filename.bz2` would show "done" instead of "ok".

**Keep the original file during compression/decompression:**

```shell
bzip2 -k filename
```

Here, adding `-k` preserves the original file; otherwise, the original file is replaced by the result. Decompression works similarly: `bzip2 -dk filename.bz2`.

**Decompress to standard output:**

```shell
bzip2 -dc filename.bz2
```

Output:

```shell
hahahhaahahha
```

Here, using `-c` specifies output to standard output, displaying the contents of `filename` without deleting `filename.bz2`.

**Compress to standard output:**

```shell
bzip2 -c filename
bzip2: I won't write compressed data to a terminal.
bzip2: For help, type: `bzip2 --help'.
```

Here, using `-c` specifies compression to standard output without deleting the original file; however, compressed data cannot be directly output to a terminal.

**Treat all subsequent arguments as files (even if they start with '-'):**

```shell
bzip2 -- -myfilename
```

This is primarily to prevent ambiguity where a filename starting with `-` might be mistaken for an option.
