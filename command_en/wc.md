wc
===

Print newline, word, and byte counts for each file

## Description

The **wc command** counts the number of bytes, words, and lines in each specified file and prints the results. If no file is specified, or if the file name is "-", it reads from standard input. It also provides a total count for all specified files.

### Syntax

```shell
wc [options] [file]...
wc [options] --files0-from=F
```

### Options

```shell
-c, --bytes  Print the byte counts.
-l, --lines  Print the newline counts.
-m, --chars  Print the character counts.
-w, --words  Print the word counts. A word is a sequence of non-zero-length characters delimited by white space.
-L, --max-line-length  Print the maximum display width (length of the longest line).
--help       Display help information.
--version    Display version information.
```

### Parameters

file: A list of files to be processed.

### Examples

Count lines, words, and bytes in a file:

```shell
wc test.txt
# Output:
7     8     70     test.txt
# Lines  Words  Bytes  Filename
```

Count lines in all files in the current directory:

```shell
wc -l *
```

Count lines in all `.js` files in the current directory:

```shell
wc -l *.js
```

Count total lines in current directory and subdirectories:

```shell
find . -type f | xargs wc -l
```

Print only the line count without the filename:

```shell
wc -l < test.txt
# Output:
7
```

Count the number of files in the current directory (excluding hidden files and total line):

```shell
expr $(ls -l | wc -l) - 1
# Output:
8
```

Example output for multiple files:

```shell
[root@centos7 ~]# wc -l *
      21 LICENSE
     270 README.md
wc: example: read: Is a directory
     785 lerna-debug.log
      25 lerna.json
wc: node_modules: read: Is a directory
   23603 package-lock.json
      79 package.json
       3 renovate.json
   24786 total
```
