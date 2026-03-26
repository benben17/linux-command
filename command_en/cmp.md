cmp
===

Compare two files for differences

## Description

The **cmp command** is used to compare two files for differences. If the two files are identical, the command produces no output. If differences are found, it identifies the character and line number of the first discrepancy. If no file name is specified or if the file name is "-", the `cmp` command reads from standard input.

### Syntax

```shell
cmp [options] [arguments]
```

### Options

```shell
-c or --print-chars: Output the differing characters in addition to their decimal codes.
-i <number> or --ignore-initial=<number>: Skip the first <number> characters of both files.
-l or --verbose: Output the byte numbers and values for all differing bytes.
-s or --quiet or --silent: Suppress all output (useful for scripts).
-v or --version: Display version information.
--help: Online help.
```

### Arguments

Files: The two files to be compared.

### Examples

To compare files "testfile" and "testfile1", use the following command:

```shell
cmp testfile testfile1            # Compare the two specified files
```

Before executing the command, you can use `cat` to view the content of both files:

```shell
cat testfile                    # View file content  
Absncn 50                       # Content of "testfile"  
Asldssja 60  
Jslkadjls 85 

cat testfile1                   # View file content  
Absncn 50                       # Content of "testfile1"  
AsldssjE 62  
Jslkadjls 85  
```

Then, execute the `cmp` command:

```shell
cmp testfile testfile1       # Compare the two files  
testfile testfile1           # Difference: byte 8, line 2  
```

Note: By default, the output only shows the first discrepancy found.
