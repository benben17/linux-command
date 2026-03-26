strings
===

Find printable strings in object files or binary files

## Description

The **strings command** searches for printable strings in object files or binary files. A string is any sequence of 4 or more printable characters ending with a newline or null character. The `strings` command is useful for identifying the content of random object files or binaries.

### Syntax

```shell
strings [ -a ] [ - ] [ -o ] [ -t Format ] [ -n Number ] [ -Number ]  [file ... ]
```

### Options

```shell
-a --all: Scan the entire file instead of just the initialized and loaded sections of the object file.
-f --print-file-name: Display the file name before each string.
-n --bytes=[number]: Find and output all sequences that are at least [number] characters long.
- : Set the minimum number of characters to display (default is 4).
-t --radix={o,d,x}: Output the offset of the string in octal, decimal, or hexadecimal.
-o: Similar to --radix=o.
-T --target=: Specify the binary file format.
-e --encoding={s,S,b,l,B,L}: Choose the character size and endianness: s = 7-bit, S = 8-bit, {b,l} = 16-bit, {B,L} = 32-bit.
@: Read options from a file.
```

### Examples

List all ASCII text in `ls`:

```shell
strings /bin/ls
```

Pipe output to strings:

```shell
cat /bin/ls | strings
```

Find strings in `ls` that contain "libc", case-insensitive:

```shell
strings /bin/ls | grep -i libc
```
