join
===

Join lines of two files on a common field.

## Description

The `join` command merges lines from two files based on a common field. It finds lines with identical content in specified fields and combines them, outputting to standard output.

### Syntax

```shell
join [options] file1 file2
```

### Options

```shell
-a <1|2> : Also print unpairable lines from file 1 or file 2.
-e <string> : Replace missing input fields with the specified string.
-i, --ignore-case : Ignore case differences when comparing fields.
-o <format> : Output according to the specified format.
-t <char> : Use the specified character as the field separator.
-v <1|2> : Like -a, but suppress joined lines.
-1 <field> : Join on this field of file 1.
-2 <field> : Join on this field of file 2.
```

### Examples

Join two files on the first field (default):

```shell
[root@localhost ~]# cat name 
1 xiaoming
2 xiaowang
[root@localhost ~]# cat city 
1 beijing
2 wuhan

[root@localhost ~]# join name city 
1 xiaoming beijing
2 xiaowang wuhan
```

Join specific columns (e.g., column 2 of file 1 and column 2 of file 2):

```shell
[root@localhost ~]# join -o 1.2 2.2 name city 
xiaoming beijing
xiaowang wuhan
```
