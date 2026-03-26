fold
===

Wrap input lines to fit a specified width.

## Description

The **fold command** is used to control the screen width occupied by file content when it is output. It reads content from the specified files and breaks any lines longer than the specified width, sending the result to standard output. If no files are specified, or if the filename is "-", `fold` reads from standard input.

### Syntax

```shell
fold (options) (parameters)
```

### Options

```shell
-b, --bytes: Count width by bytes instead of columns.
-s, --spaces: Break lines at spaces if possible.
-w <width>, --width=<width>: Set the maximum line width (default is 80).
```

### Parameters

File: Specifies the file whose content is to be displayed.

### Example

```shell
fold -w 5 filename
```
