uniq
===

Report or omit repeated lines.

## Synopsis

```shell
uniq [OPTION]... [INPUT [OUTPUT]]
```

## Main Uses

- Write adjacent duplicate lines from the input file (or standard input) to the output file (or standard output).
- When no options are provided, adjacent duplicate lines are merged into one.

## Options

```shell
-c, --count                Prefix lines by the number of occurrences.
-d, --repeated             Only print duplicate lines, one for each group.
-D                         Print all duplicate lines.
--all-repeated[=METHOD]    Like -D, but allow groups to be delimited by an empty line. METHOD={none(default), prepend, separate}.
-f, --skip-fields=N        Avoid comparing the first N fields.
--group[=METHOD]           Show all lines, separating groups with an empty line. METHOD={separate(default), prepend, append, both}.
-i, --ignore-case          Ignore differences in case when comparing.
-s, --skip-chars=N         Avoid comparing the first N characters.
-u, --unique               Only print unique lines (those that are not repeated adjacently).
-z, --zero-terminated      Line delimiter is NUL, not newline.
-w, --check-chars=N        Compare no more than N characters in lines.
--help                     Display help information and exit.
--version                  Display version information and exit.
```

## Parameters

INPUT (optional): Input file; if not provided, standard input is used.

OUTPUT (optional): Output file; if not provided, standard output is used.

## Return Value

Returns 0 on success, and a non-zero value on failure.

## Examples

Note: Commands 2 and 3 produce the same result; command 1 only de-duplicates adjacent lines.

```shell
uniq file.txt
sort file.txt | uniq
sort -u file.txt
```

Only display unique lines; the difference is whether sorting is performed:

```shell
uniq -u file.txt
sort file.txt | uniq -u
```

Count the number of occurrences of each line in the file:

```shell
sort file.txt | uniq -c
```

Find duplicate lines in a file:

```shell
sort file.txt | uniq -d
```

### Note

1. `uniq` only detects if adjacent lines are duplicates; `sort -u` sorts the input file before processing duplicate lines.

2. This command is part of the `GNU coreutils` package. For related help information, please see `man -s 1 uniq` or `info coreutils 'uniq invocation'`.
