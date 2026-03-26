cut
===

Remove sections from each line of files

## Supplemental Information

The **cut command** is used to display specific parts of lines and remove specified fields from a file. It is frequently used to extract columns from a text file or piped data.

Note: The `cut` command's primary function is to cut out selected portions of each line of a file and write the result to standard output. It can use bytes (`-b`), characters (`-c`), or fields (`-f`) delimited by a character (`-d`).

### Syntax

```shell
cut (options) (parameters)
```

### Options

```shell
-b: Select only these bytes;
-c: Select only these characters;
-d: Use delimiter instead of TAB for field delimiter;
-f: Select only these fields; also print any line that contains no delimiter character, unless the -s option is specified;
-n: (with -b) do not split multi-byte characters;
--complement: Complement the set of selected bytes, characters or fields;
--out-delimiter=STRING: Use STRING as the output delimiter;
--help: Display help information;
--version: Display version information.
```

### Parameters

File: The file to be filtered.

### Examples

Given a student report with No, Name, Mark, and Percent:

```shell
[root@localhost text]# cat test.txt
No Name Mark Percent
01 tom 69 91
02 jack 71 87
03 alex 68 98
```

Use the **-f** option to extract specific fields:

```shell
[root@localhost text]# cut -f 1 test.txt
No
01
02
03
```

```shell
[root@localhost text]# cut -f2,3 test.txt
Name Mark
tom 69
jack 71
alex 68
```

Use the **--complement** option to extract all columns except the specified ones:

```shell
[root@localhost text]# cut -f2 --complement test.txt
No Mark Percent
01 69 91
02 71 87
03 68 98
```

Use the **-d** option to specify a field delimiter:

```shell
[root@localhost text]# cat test2.txt
No;Name;Mark;Percent
01;tom;69;91
02;jack;71;87
03;alex;68;98
```

```shell
[root@localhost text]# cut -f2 -d";" test2.txt
Name
tom
jack
alex
```

### Specifying Character or Byte Ranges

The cut command can display a range of characters or bytes:

* **N-**: From the Nth byte/character/field to the end of the line;
* **N-M**: From the Nth to the Mth (inclusive) byte/character/field;
* **-M**: From the 1st to the Mth (inclusive) byte/character/field.

Combine these with the following options:

* **-b**: Bytes;
* **-c**: Characters;
* **-f**: Fields.

**Examples**

```shell
[root@localhost text]# cat test.txt
abcdefghijklmnopqrstuvwxyz
abcdefghijklmnopqrstuvwxyz
abcdefghijklmnopqrstuvwxyz
abcdefghijklmnopqrstuvwxyz
abcdefghijklmnopqrstuvwxyz
```

Print the 1st to 3rd characters:

```shell
[root@localhost text]# cut -c1-3 test.txt
abc
abc
abc
abc
abc
```

Print the first 2 characters:

```shell
[root@localhost text]# cut -c-2 test.txt
ab
ab
ab
ab
ab
```

Print from the 5th character to the end:

```shell
[root@localhost text]# cut -c5- test.txt
efghijklmnopqrstuvwxyz
efghijklmnopqrstuvwxyz
efghijklmnopqrstuvwxyz
efghijklmnopqrstuvwxyz
efghijklmnopqrstuvwxyz
```

Print the last 5 characters:

Unfortunately, `cut` does not directly support counting from the end. However, this can be achieved by reversing the string:

```shell
[root@localhost text]# cat test.txt | rev | cut -c -5 | rev
vwxyz
vwxyz
vwxyz
vwxyz
vwxyz
```
