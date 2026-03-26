zcat
===

Display the contents of files inside a compressed archive

## Description

The **zcat** command is used to display the contents of a compressed file without actually decompressing it.

### Syntax

```shell
zcat [options] [parameters]
```

### Options

```shell
-S, --suffix=[suffix]: Specify the suffix for gzip compressed files. Use this option when the suffix is not a standard compression suffix;
-c, --stdout: Write the file content to standard output;
-d, --decompress: Perform decompression;
-l, --list: List the files inside the compressed archive;
-L, --license: Display software license information;
-q, --quiet: Suppress warning messages;
-r, --recursive: Perform recursive operations on directories;
-t, --test: Test the integrity of compressed files;
-V, --version: Display version information;
-1, --fast: Faster compression speed;
-9, --best: Higher compression ratio.
```

### Parameters

Files: Specifies the compressed archives whose contents are to be displayed.
