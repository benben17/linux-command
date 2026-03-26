comm
===

Compare two sorted files line by line.

## Synopsis

```shell
comm [OPTION]... FILE1 FILE2
```

## Main Purpose

- Compare two sorted files line by line.
- Read from standard input when `FILE1` or `FILE2` is `-`.
- Without options, output three columns: lines unique to `FILE1`, lines unique to `FILE2`, and lines common to both.

## Options

```shell
-1                        Suppress column 1 (lines unique to FILE1).
-2                        Suppress column 2 (lines unique to FILE2).
-3                        Suppress column 3 (lines common to both).
--check-order             Check that the input is correctly sorted, even if all input lines are paired.
--nocheck-order           Do not check that the input is correctly sorted.
--output-delimiter=STR    Use STR as the separator between output columns instead of the default TAB.
--total                   Output a fourth column containing a summary.
-z, --zero-terminated     Set line delimiter to NUL instead of newline.
--help                    Display help information and exit.
--version                 Display version information and exit.
```

## Return Value

Returns 0 on success, and non-zero on failure.

## Examples

Content of `aaa.txt`:

```shell
[root@localhost text]# cat aaa.txt 
aaa
bbb
ccc
ddd
eee
111
222
```

Content of `bbb.txt`:

```shell
[root@localhost text]# cat bbb.txt 
bbb
ccc
aaa
hhh
ttt
jjj
```

Comparison result:

```shell
[root@localhost text]# comm --nocheck-order aaa.txt bbb.txt 
aaa
                bbb
                ccc
        aaa
ddd
eee
111
222
        hhh
        ttt
        jjj
```

The first column contains lines only in `aaa.txt`, the second column contains lines only in `bbb.txt`, and the third column contains lines common to both. TAB (\t) is used as the default separator between columns.

### Comparing Sorted Files

First, sort the file contents using `sort`:

```shell
[root@localhost ~]# sort aaa.txt > aaa1.txt
[root@localhost ~]# sort bbb.txt > bbb1.txt
```

Comparison result:

```shell
[root@localhost ~]# comm aaa1.txt bbb1.txt
111
222
		aaa
		bbb
		ccc
ddd
eee
	hhh
	jjj
	ttt
```

### Intersection

To print the intersection of two files, suppress the first and second columns:

```shell
[root@localhost text]# comm aaa.txt bbb.txt -1 -2
bbb
ccc
```

### Difference

By suppressing unwanted columns, you can obtain the difference between `aaa.txt` and `bbb.txt`:

Lines unique to `aaa.txt`:

```shell
[root@localhost text]# comm aaa.txt bbb.txt -2 -3
aaa
ddd
eee
111
222
```

Lines unique to `bbb.txt`:

```shell
[root@localhost text]# comm aaa.txt bbb.txt -1 -3
aaa
hhh
ttt
jjj
```

### Note

1. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 comm` or `info coreutils 'comm invocation'`.
观察
