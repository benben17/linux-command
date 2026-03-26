nl
===

Number lines of files

## Synopsis

```shell
nl [OPTION]... [FILE]...
```

## Description

- Write each FILE to standard output, with line numbers added.
- With no FILE, or when FILE is `-`, read standard input.
- Handles logical pages.

## Options

```shell
-b, --body-numbering=STYLE           Use STYLE for numbering body lines.
-d, --section-delimiter=CC           Use CC for separating logical pages.
-f, --footer-numbering=STYLE         Use STYLE for numbering footer lines.
-h, --header-numbering=STYLE         Use STYLE for numbering header lines.
-i, --line-increment=NUMBER          Line number increment at each line.
-l, --join-blank-lines=NUMBER        Group of NUMBER empty lines counted as one.
-n, --number-format=FORMAT           Insert line numbers according to FORMAT.
-p, --no-renumber                    Do not reset line numbers at logical pages.
-s, --number-separator=STRING        Add STRING after the line number.
-v, --starting-line-number=NUMBER    First line number on each logical page.
-w, --number-width=NUMBER            Use NUMBER columns for line numbers.
--help                               Display help message and exit.
--version                            Display version information and exit.


Default options are: -bt -d'\:' -fn -hn -i1 -l1 -nrn -sTAB -v1 -w6

CC consists of two characters; default is \: . If the second character is missing, it defaults to :.

STYLE can be one of:

a       Number all lines.
t       Number only non-empty lines.
n       Do not number lines.
pBRE    Number only lines that match the basic regular expression (BRE).

FORMAT can be one of:

ln    Left justified, no leading zeros.
rn    Right justified, no leading zeros.
rz    Right justified, leading zeros.

Logical Page Structure:
Consists of three sections: header, body, and footer.
Delimiters: header \:\:\:, body \:\:, footer \:
```

## Parameters

FILE (optional): One or more files to be processed.

## Return Value

Returns 0 on success, non-zero on failure.

## Examples

```shell
nl_logicalpage.txt: This file is used to demonstrate logical page handling.
\:\:\:
header_1
\:\:
body_1
\:
footer_1
\:\:\:
header_2
\:\:
body_2
\:
footer_2
```

```shell
[user2@pc ~]$ nl nl_logicalpage.txt

       header_1

     1	body_1

       footer_1

       header_2

     1	body_2

       footer_2

[user2@pc ~]$ nl -v0 -fa -ha nl_logicalpage.txt

     0	header_1

     1	body_1

     2	footer_1

     0	header_2

     1	body_2

     2	footer_2

[user2@pc ~]$ nl -p -fa -ha nl_logicalpage.txt

     1	header_1

     2	body_1

     3	footer_1

     4	header_2

     5	body_2

     6	footer_2
```

```shell
nl_normal.txt: Example of a normal file.
ZhuangZhu-74
2019-11-21
127.0.0.1
```

```shell
[user2@pc ~]$ nl nl_normal.txt
     1	ZhuangZhu-74
     2	2019-11-21
     3	127.0.0.1

[user2@pc ~]$ nl -b p'1$' nl_normal.txt
       ZhuangZhu-74
     1	2019-11-21
     2	127.0.0.1

[user2@pc ~]$ nl -b p'^[A-Z]' nl_normal.txt
     1	ZhuangZhu-74
       2019-11-21
       127.0.0.1
```

### Notes

1. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 nl` or `info coreutils 'nl invocation'`.
