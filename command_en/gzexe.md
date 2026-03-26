gzexe
===

Compress executable files.

## Supplemental Information

The **gzexe command** is used to compress executable files. The resulting files remain executable and automatically decompress when run. When you execute a compressed file, it decompresses itself and then continues execution, behaving identically to a normal executable. This command can be thought of as an extension to the `gunzip` utility.

### Syntax

```shell
gzexe (options) (parameters)
```

### Options

```shell
-d: Decompress an executable file previously compressed with gzexe.
```

### Parameters

File: Specifies the executable file to be compressed.
