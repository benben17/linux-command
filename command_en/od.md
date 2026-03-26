od
===

Output files in octal, hexadecimal, and other formats.

## Description

The **od command** is used to output the contents of a file in octal, hexadecimal, or other encoded formats. It is typically used to display or inspect characters in a file that cannot be directly displayed in the terminal.

Common files are either text or binary. This command is primarily used to view values stored in binary files. For instance, if a program outputs a large number of single-precision floating-point records to a file, the `od` command can be used to inspect these values. It provides an unambiguous interpretation of the data in a file, whether it's IEEE 754 floating-point numbers or ASCII codes.

### Syntax

```shell
od [options] [file...]
```

### Options

```shell
-a                            # Same as -t a (named characters).
-A <radix>                    # Choose the input offset radix: d (decimal), o (octal), x (hexadecimal), or n (none).
-b                            # Same as -t oC (octal bytes).
-c                            # Same as -t c (ASCII characters or backslash escapes).
-d                            # Same as -t u2 (unsigned decimal 2-byte units).
-f                            # Same as -t fF (floats).
-h                            # Same as -t x2 (hexadecimal 2-byte units).
-i                            # Same as -t d2 (signed decimal 2-byte units).
-j <bytes>, --skip-bytes=<bytes> # Skip the specified number of bytes from the beginning of the input.
-l                            # Same as -t d4 (signed decimal 4-byte units).
-N <bytes>, --read-bytes=<bytes> # Limit the output to the specified number of bytes.
-o                            # Same as -t o2 (octal 2-byte units).
-s <bytes>, --strings=<bytes> # Output strings of at least the specified number of graphic characters.
-t <type>, --format=<type>    # Select the output format.
-v, --output-duplicates       # Do not use * to mark line suppression (output all duplicate data).
-w <bytes>, --width=<bytes>   # Set the number of output bytes per line.
-x                            # Same as -t x2 (hexadecimal 2-byte units).
--help                        # Display help information.
--version                     # Display version information.
```

### Parameters

File: The file(s) to be displayed.

### Examples

Prepare a sample file `tmp`:

```shell
[user@localhost ~]$ echo "abcdef g" > tmp
[user@localhost ~]$ cat tmp
abcdef g
```

Output using single-byte octal interpretation:

```shell
[user@localhost ~]$ od -b tmp
0000000 141 142 143 144 145 146 040 147 012
0000011
```

Output using ASCII characters (including escape sequences):

```shell
[user@localhost ~]$ od -c tmp
0000000   a   b   c   d   e   f       g  \n
0000011
```

Output using single-byte decimal interpretation:

```shell
[user@localhost ~]$ od -t d1 tmp
0000000   97   98   99  100  101  102   32  103   10
0000011
```

Set the address (offset) radix to decimal:

```shell
[user@localhost ~]$ od -A d -c tmp
0000000   a   b   c   d   e   f       g  \n
0000009
```

Set the address (offset) radix to hexadecimal:

```shell
[user@localhost ~]$ od -A x -c tmp
000000   a   b   c   d   e   f       g  \n
0000009
```

Skip the first two bytes:

```shell
[user@localhost ~]$ od -j 2 -c tmp
0000002   c   d   e   f       g  \n
0000011
```

Skip the first two bytes and output only two bytes:

```shell
[user@localhost ~]$ od -N 2 -j 2 -c tmp
0000002   c   d
0000004
```

Output one byte per line:

```shell
[user@localhost ~]$ od -w1 -c tmp
0000000   a
0000001   b
0000002   c
0000003   d
0000004   e
0000005   f
0000006   
0000007   g
0000010  \n
0000011
```

Output two bytes per line:

```shell
[user@localhost ~]$ od -w2 -c tmp
0000000   a   b
0000002   c   d
0000004   e   f
0000006       g
0000010  \n
0000011
```

Output three bytes per line using octal single-byte interpretation:

```shell
[user@localhost ~]$ od -w3 -b tmp
0000000 141 142 143
0000003 144 145 146
0000006 040 147 012
0000011
```
