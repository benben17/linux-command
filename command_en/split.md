split
===

Split a file into pieces.

## Description

The **split command** is used to split a large file into smaller pieces. This is often done to improve readability, manage logs, or meet file size constraints for transfer.

### Options

```shell
-b: Size of each output file (units can be k, m, etc.; default unit is bytes).
-C: Maximum number of bytes per line in each output file.
-d: Use numeric suffixes instead of alphabetic ones.
-l: Number of lines per output file.
-a: Length of the suffix (default is 2).
```

### Examples

Generate a 100KB test file:

```shell
[root@localhost split]# dd if=/dev/zero bs=100k count=1 of=date.file
1+0 records in
1+0 records out
102400 bytes (102 kB) copied, 0.00043 seconds, 238 MB/s
```

Use the split command to split the `date.file` into 10KB pieces:

```shell
[root@localhost split]# split -b 10k date.file 
[root@localhost split]# ls
date.file  xaa  xab  xac  xad  xae  xaf  xag  xah  xai  xaj
```

The files are created with alphabetic suffixes. To use numeric suffixes and specify the suffix length:

```shell
[root@localhost split]# split -b 10k date.file -d -a 3
[root@localhost split]# ls
date.file  x000  x001  x002  x003  x004  x005  x006  x007  x008  x009
```

Specify a filename prefix for the split files:

```shell
[root@localhost split]# split -b 10k date.file -d -a 3 split_file
[root@localhost split]# ls
date.file  split_file000  split_file001  split_file002  split_file003  split_file004  split_file005  split_file006  split_file007  split_file008  split_file009
```

Use the `-l` option to split the file based on the number of lines (e.g., 10 lines per file):

```shell
split -l 10 date.file
```
