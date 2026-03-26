col
===

Filter control characters from input

## Description

The **col command** is a standard input text filter that reads from standard input and writes to standard output. Many UNIX manual pages contain reverse line feed (RLF) control characters. When using shell redirection characters `>` and `>>` to save a manual page to a plain text file, these control characters can result in garbled text. The `col` command effectively filters out these control characters.

### Syntax

```shell
col [options]
```

### Options

```shell
-b: Filter out all control characters, including RLF and HRLF (Half Reverse Line Feed).
-f: Filter out RLF but allow HRLF to be displayed.
-x: Convert tabs to spaces.
-l <number>: Specify the number of lines to buffer in memory (default is 128).
```
