tac
===

Concatenate and print files in reverse line by line

## Summary

```shell
tac [OPTION]... [FILE]...
```

## Description

- Reverses the order of lines in a file and prints them to standard output. If no file is specified or if the file is `-`, it reads from standard input.
- When processing multiple files, it reverses each file individually rather than concatenating them all before reversing.

### Parameters

FILE (optional): One or more files to process.

### Options 

```shell
-b, --before              Attach the separator before rather than after.
-r, --regex               Treat the separator as a Basic Regular Expression (BRE).
-s, --separator=STRING    Use STRING as the separator instead of the default newline.
--help                    Display help and exit.
--version                 Display version information and exit.
```

## Return Value

Returns success unless invalid options or parameters are provided.

## Examples 

```shell
# Reverse a file character by character (example from info docs):
tac -r -s 'x\|[^x]' test.log

# About the -b option:
seq 1 3 | tac
# Output
3
2
1

# Using the -b option:
seq 1 3 | tac -b
# Output (note there is no newline after 21)


3
21

# The first example converts '1\n2\n3\n' to '3\n2\n1\n'
# The second example converts '1\n2\n3\n' to '\n\n3\n21'
```

### Notes

1. This command is part of the `GNU coreutils` package. See `man -s 1 tac` or `info coreutils 'tac invocation'` for more information.
2. For details on Basic Regular Expressions (BRE), see the `REGULAR EXPRESSIONS` section in `man -s 1 grep`.
