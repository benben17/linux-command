sha256sum
===

Used to calculate the SHA-256 hash value of files.

## Description

The **sha256sum command** prints or checks SHA256 (256-bit) checksums.

### Syntax

```shell
sha256sum [OPTION]... [FILE]...
```

### Options

```shell
-b, --binary  # read in binary mode
-c, --check   # read SHA256 sums from the FILEs and check them
    --tag     # create a BSD-style checksum
-t, --text    # read in text mode (default)
-z, --zero    # end each output line with NUL, not newline, and disable file name escaping
    --help    # display this help and exit
    --version # output version information and exit
```

### Examples

Here are some examples of using the sha256sum command:

1. Calculate the SHA-256 hash value of a file:

```shell
sha256sum file.txt
```

This will output the SHA-256 hash value of file.txt and the filename.

2. Calculate the SHA-256 hash values of multiple files:

```shell
sha256sum file1.txt file2.txt
```

This will output the SHA-256 hash values of file1.txt and file2.txt and their filenames.

3. Save the SHA-256 hash value to a file:

```shell
sha256sum file.txt > hash.txt
```

This will save the SHA-256 hash value of file.txt into the file hash.txt.

4. Verify the SHA-256 hash value of a file:

```shell
sha256sum -c hash.txt
```

This will verify whether the SHA-256 hash value of the file matches the value in hash.txt. If it matches, it outputs OK; otherwise, it outputs FAILED.
