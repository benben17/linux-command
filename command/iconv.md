iconv
===

Convert text from one character encoding to another.

## Description

The `iconv` command is used to convert the encoding of files. For example, it can convert UTF-8 encoded files to GB18030 and vice versa. Similar tools include JDK's `native2ascii`. The `iconv` library in Linux includes C functions like `iconv_open`, `iconv_close`, and `iconv`, which are useful for character conversion in C/C++ programs, especially when web scraping. The `iconv` command is helpful for debugging such programs.

### Syntax

```shell
iconv -f encoding [-t encoding] [inputfile]... 
```

### Options

```shell
-f encoding : Specify the source encoding.
-t encoding : Specify the target encoding.
-l : List all known coded character sets.
-o file : Specify the output file.
-c : Silently discard characters that cannot be converted instead of terminating.
-s : Suppress warning messages.
--verbose : Display progress information.
```

The valid encodings for `-f` and `-t` can be listed using the `-l` option.

### Examples

List all supported character encodings:

```shell
iconv -l 
```

Convert `file1` from EUC-JP-MS to UTF-8 and save the output to `file2`:

```shell
iconv file1 -f EUC-JP-MS -t UTF-8 -o file2 
```

If `-o` is not specified, the output is sent to standard output (stdout).
