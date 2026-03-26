dirname
===

Strip the non-directory suffix from a file name.

## Description

The **dirname** command removes the non-directory part of a file name, displaying only the content related to the directory. It reads the specified path, retains everything before the last `/`, deletes the rest, and writes the result to standard output. If there are no characters after the last `/`, dirname uses the second-to-last `/` and ignores everything after it. `dirname` and `basename` are commonly used in shell command substitution to specify an output filename slightly different from the input filename.

### Syntax

```shell
dirname (options) (parameters)
```

### Options

```shell
--help     Display help.
--version  Display version information.
```

### Examples

```shell
dirname //
Result: /

dirname /a/b/
Result: /a

dirname a
Result: .

dirname a/b
Result: a
```
