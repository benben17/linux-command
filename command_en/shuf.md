shuf
===

Generate random permutations.

## Synopsis

```shell
shuf [OPTION]... [FILE]
shuf -e [OPTION]... [ARG]...
shuf -i LO-HI [OPTION]...
```

## Main Description

- Randomly permutes input lines and writes them to standard output.
- When no file is specified or the file is `-`, it reads from standard input.

## Options

```shell
-e, --echo                  Treat each ARG as an input line.
-i, --input-range=LO-HI     Treat each number LO through HI as an input line.
-n, --head-count=COUNT      Output at most COUNT lines.
-o, --output=FILE           Write the result to FILE instead of standard output.
    --random-source=FILE    Get random bytes from FILE.
-r, --repeat                Output lines can be repeated.
-z, --zero-terminated       Line delimiter is NUL (null character) instead of the default newline.
--help                      Display help information and exit.
--version                   Output version information and exit.
```

## Parameters

FILE (optional): The file to process, multiple files can be specified.

ARG (optional): Strings to be treated as input lines, multiple arguments can be specified.

## Return Value

Returns 0 for success, and a non-zero value for failure.

## Examples

```shell
# Simulate a coin toss and get the first 10 results:
[user2@pc ~]$ shuf -r -n 10 -e "Heads" -e "Tails"
Tails
Heads
Heads
Heads
Tails
Tails
Tails
Heads
Heads
Heads
```

```shell
[user2@pc ~]$ shuf -i 1-35 -n 5|sort -n && shuf -i 1-12 -n 2|sort -n
4
17
20
29
31
6
11
```

### Note

1. This command is part of the `GNU coreutils` package. For more detailed help, please check `man -s 1 shuf` or `info coreutils 'shuf invocation'`.
