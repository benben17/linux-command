diff3
===

Compare three files line by line.

## Description

The **diff3** command compares three files and displays the differences between them to standard output.

### Syntax

```shell
diff3 (options) (parameters)
```

### Options

```shell
-a           Treat all files as text and compare them line by line, even if they are not text files.
-A           Incorporate all changes from file2 to file3 into file1, marking conflicts with brackets.
-B           Same as -A, but do not display conflicting changes.
-e, --ed     Output an ed script that can be used to incorporate all changes from file2 to file3 into file1.
--easy-only  Like -e, but incorporate only non-overlapping changes.
-i           Append 'w' and 'q' commands to ed scripts for System V compatibility. Must be used with -AeExX3, cannot be used with -m.
--initial-tab Prepend a tab instead of two spaces to lines of normal format. This makes tab alignment look more standard.
```

### Parameters

* File 1: Specifies the first file to compare.
* File 2: Specifies the second file to compare.
* File 3: Specifies the third file to compare.
