unzip
===

Used to decompress archives compressed by the zip command.

## Description

The **unzip command** is used to decompress ".zip" archives created by the zip command.

### Syntax

```shell
unzip (option) (parameter)
```

### Options

```shell
-c: Display decompression results on the screen and perform appropriate character conversion;
-f: Update existing files;
-l: List the files contained within the compressed file;
-p: Similar to the -c parameter, displays decompression results on the screen but without any conversion;
-t: Test the integrity of the compressed file;
-u: Similar to the -f parameter, but in addition to updating existing files, it also decompresses other files from the archive into the directory;
-v: Display detailed information during execution;
-z: Display only the comments of the compressed file;
-a: Perform necessary character conversion for text files;
-b: Do not perform character conversion for text files;
-C: Filenames in the compressed file are case-sensitive;
-j: Do not process the original directory paths in the compressed file;
-L: Convert all filenames in the compressed file to lowercase;
-M: Pipe output through the more program;
-n: Do not overwrite existing files during decompression;
-o: Overwrite existing files without prompting the user;
-P<password>: Use the password option for zip;
-q: Run quietly, displaying no information;
-s: Convert whitespace characters in filenames to underscores;
-V: Retain VMS file version information;
-X: Restore original file UID/GID during decompression;
-d<directory>: Specify the directory where files should be stored after decompression;
-x<file>: Specify files in the .zip archive that should not be processed;
-Z: unzip -Z is equivalent to executing the zipinfo command.
```

### Parameters

Archive: Specifies the ".zip" archive to be decompressed.

### Examples

Decompress `test.zip` in the current directory:

```shell
unzip test.zip
```

Decompress `test.zip` into the specified directory `/tmp`, and do not overwrite existing files:

```shell
unzip -n test.zip -d /tmp
```

View the contents of the compressed file without decompressing:

```shell
unzip -v test.zip
```

Decompress `test.zip` into the specified directory `/tmp`, and overwrite existing files:

```shell
unzip -o test.zip -d /tmp/
```

Decompress specific files, using * as a wildcard:

```shell
unzip test.zip "*.jpg"
```
