realpath
========

Resolve and canonicalize file paths, returning the absolute path.

## Description

The **realpath** command resolves symbolic links and relative paths (e.g., `.`, `..`) in a given path and outputs the corresponding **absolute path**. It is commonly used in scripts to obtain the true location of a file or directory, avoiding path ambiguity caused by symbolic links or relative paths.

Unlike simply using `pwd` or string concatenation, `realpath` ensures that the output path is a unique, real, and accessible physical path.

### Syntax

```shell
realpath [options] file...
```

### Options

```shell
-e, --canonicalize-existing   Only output if all components of the path exist.
-m, --canonicalize-missing    Output the canonicalized path even if components do not exist.
-L, --logical                 Resolve symbolic links logically (default).
-P, --physical                Resolve symbolic links physically.
-q, --quiet                   Quiet mode; do not output error messages.
-s, --strip-trailing-slashes  Remove trailing slashes from the path.
--relative-to=DIR             Output the path relative to DIR.
--relative-base=DIR           If possible, output the path relative to DIR.
--help                        Display help information.
--version                     Display version information.
```

### Parameters

```shell
file               The path of the file or directory to be resolved, which can be a relative path or a symbolic link.
```

## Examples

### Get the absolute path of a file

```shell
realpath file.txt
```

### Resolve the real path of a symbolic link

```shell
realpath /usr/bin/python
```

### Return a canonicalized result even if the path does not exist

```shell
realpath -m ./non/existent/path
```

### Output path relative to a specified directory

```shell
realpath --relative-to=/usr /usr/bin/env
```
