sort
===

Sort lines of text files.

## Synopsis

```shell
sort [OPTION]... [FILE]...
sort [OPTION]... --files0-from=F
```

## Main Description

- Writes sorted concatenation of all FILE(s) to standard output.
- With no FILE, or when FILE is `-`, it reads from standard input.

## Options

Sorting options:
```shell
-b, --ignore-leading-blanks    Ignore leading blanks.
-d, --dictionary-order         Consider only blanks and alphanumeric characters.
-f, --ignore-case              Fold lower case to upper case characters.
-g, --general-numeric-sort     Compare according to general numerical value.
-i, --ignore-nonprinting       Consider only printable characters.
-M, --month-sort               Compare (unknown) < 'JAN' < ... < 'DEC'.
-h, --human-numeric-sort       Compare human-readable numbers (e.g., 2K, 1G).
-n, --numeric-sort             Compare according to string numerical value.
-R, --random-sort              Shuffle, but group identical keys.
--random-source=FILE           Get random bytes from FILE.
-r, --reverse                  Reverse the result of comparisons.
--sort=WORD                    Sort according to WORD: general-numeric (-g), human-numeric (-h), month (-M), numeric (-n), random (-R), version (-V).
-V, --version-sort             Natural sort of (version) numbers within text.
```

Other options:
```shell
--batch-size=NMERGE                    Merge at most NMERGE inputs at once; for more, use temporary files.
-c, --check, --check=diagnose-first    Check for sorted input; do not sort.
-C, --check=quiet, --check=silent      Like -c, but do not report the first unsorted line.
--compress-program=PROG                Compress temporary files with PROG; decompress them with PROG -d.
--debug                                Annotate the part of the line used to sort, and warn about questionable usage to stderr.
--files0-from=F                        Read input from the files specified by NUL-terminated names in file F; if F is -, then read names from standard input.
-k, --key=KEYDEF                       Sort via a key; KEYDEF gives location and type.
-m, --merge                            Merge already sorted files; do not sort.
-o, --output=FILE                      Write result to FILE instead of standard output.
-s, --stable                           Stabilize sort by disabling last-resort comparison.
-S, --buffer-size=SIZE                 Use SIZE for main memory buffer.
-t, --field-separator=SEP              Use SEP instead of non-blank to blank transition as field separator.
-T, --temporary-directory=DIR          Use DIR for temporary files, not $TMPDIR or /tmp; multiple options specify multiple directories.
--parallel=N                           Change the number of sorts run concurrently to N.
-u, --unique                           With -c, check for strict ordering; without -c, output only the first of an equal run.
-z, --zero-terminated                  Line delimiter is NUL, not newline.
--help                                 Display help information and exit.
--version                              Output version information and exit.

The format of KEYDEF is: F[.C][OPTS][,F[.C][OPTS]], which represents the start to end positions.
F indicates the field number.
C indicates the character position within the field.
OPTS is one or more single-letter ordering options [bdfgiMhnRrV], which override global ordering options for that key.
Use the --debug option to diagnose incorrect usage.

SIZE can have the following multiplicative suffixes:
% 1% of memory;
b 1;
K 1024 (default);
Remaining M, G, T, P, E, Z, Y follow the same pattern.
```

## Parameters

FILE (optional): The files to be processed, multiple files can be specified.

## Return Value

Returns 0 for success, and a non-zero value for failure.

## Examples

`sort` compares each line of a file/text as a unit. The comparison is done character by character based on ASCII values, and the lines are output in ascending order.

```shell
root@[mail text]# cat sort.txt
aaa:10:1.1
ccc:30:3.3
ddd:40:4.4
bbb:20:2.2
eee:50:5.5
eee:50:5.5

[root@mail text]# sort sort.txt
aaa:10:1.1
bbb:20:2.2
ccc:30:3.3
ddd:40:4.4
eee:50:5.5
eee:50:5.5
```

Ignore duplicate lines using the `-u` option or the `uniq` command:

```shell
[root@mail text]# cat sort.txt
aaa:10:1.1
ccc:30:3.3
ddd:40:4.4
bbb:20:2.2
eee:50:5.5
eee:50:5.5

[root@mail text]# sort -u sort.txt
aaa:10:1.1
bbb:20:2.2
ccc:30:3.3
ddd:40:4.4
eee:50:5.5

[root@mail text]# uniq sort.txt
aaa:10:1.1
ccc:30:3.3
ddd:40:4.4
bbb:20:2.2
eee:50:5.5
```

Using the `-n`, `-r`, `-k`, and `-t` options of `sort`:

```shell
[root@mail text]# cat sort.txt
AAA:BB:CC
aaa:30:1.6
ccc:50:3.3
ddd:20:4.2
bbb:10:2.5
eee:40:5.4
eee:60:5.1

# Sort the BB column numerically in ascending order:
[root@mail text]# sort -nk 2 -t: sort.txt
AAA:BB:CC
bbb:10:2.5
ddd:20:4.2
aaa:30:1.6
eee:40:5.4
ccc:50:3.3
eee:60:5.1

# Sort the CC column numerically in descending order:
# -n for numeric sort, -r for reverse order, -k for field, -t for delimiter
[root@mail text]# sort -nrk 3 -t: sort.txt
eee:40:5.4
eee:60:5.1
ddd:20:4.2
ccc:50:3.3
bbb:10:2.5
aaa:30:1.6
AAA:BB:CC
```

Interpretation and examples of the `-k` option:

Detailed interpretation of the -k option:

```shell
FStart.CStart Modifier,FEnd.CEnd Modifier
-------Start--------,-------End--------
 FStart.CStart Option ,  FEnd.CEnd Option
```

This syntax format is divided into two main parts by a comma: the **Start** part and the **End** part.
The Start part consists of three sub-parts, where the Modifier part is the option part we discussed earlier.
Focusing on `FStart` and `C.Start` in the `Start` part: `C.Start` can be omitted, which means starting from the beginning of the field. `FStart.CStart` means: `FStart` is the field to use, and `CStart` is the character position within `FStart` to start sorting.
Similarly, in the End part, you can set `FEnd.CEnd`. If you omit `.CEnd` or set it to 0, it means the end of the field.

Example: Sort starting from the second letter of the company's English name:

```shell
$ sort -t ' ' -k 1.2 facebook.txt
baidu 100 5000
sohu 100 4500
google 110 5000
guge 50 3000
```

Explanation: Using `-k 1.2` means sorting the string starting from the second character of the first field to the end of the field. You'll find "baidu" at the top because its second letter is 'a'. Both "sohu" and "google" have 'o' as their second character, but 'h' in "sohu" comes before 'o' in "google", so they are second and third respectively. "guge" is fourth.

Example: Sort only by the second letter of the company name; if they are the same, sort by employee salary in descending order:

```shell
$ sort -t ' ' -k 1.2,1.2 -nrk 3,3 facebook.txt
baidu 100 5000
google 110 5000
sohu 100 4500
guge 50 3000
```

Explanation: Since we only want to sort by the second letter, we use `-k 1.2,1.2`. If we used `-k 1.2`, it would sort from the second letter to the end of the field. For employee salary, we use `-k 3,3` to sort only by the third field.

### Notes

1. [Difference between -g and -n options: stackoverflow](https://stackoverflow.com/questions/1255782/whats-the-difference-between-general-numeric-sort-and-numeric-sort-options)
2. For more complex usage, refer to the info documentation or community resources.
3. This command is part of the `GNU coreutils` package. For more details, see `man -s 1 sort` or `info coreutils 'sort invocation'`.
