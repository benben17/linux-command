nm
===

List symbols from object files

## Description

The **nm command** is used to display the symbol table from binary object files.

### Syntax

```shell
nm [options] [file...]
```

### Options

```shell
-A: Precede each symbol by the name of the input file.
-D: Display dynamic symbols instead of normal symbols.
-g: Display only external (global) symbols.
-r: Sort symbols in reverse order.
```

### Parameters

Object file: Binary object files, typically library files (.a, .so) or executables.
