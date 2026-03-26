ld
===

Link object files into an executable program

## Description

The **ld** command is the GNU linker, which links object files into an executable program.

### Syntax

```shell
ld (options) (parameters)
ld [options] objfile ...
```

### Options

```shell
-o: Specify the output filename;
-e: Specify the entry point symbol of the program.
```

### Parameters

Object file: Specify the object files to be linked.

### Examples

This tells `ld` to produce a file called `output` by linking the file `/lib/crt0.o` with `hello.o` and the library `libc.a`, which will come from the standard search directories.

```shell
ld -o <output> /lib/crt0.o hello.o -lc
ld -o output /lib/crt0.o hello.o -lc
```
