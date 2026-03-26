diff
===

Compare files line by line.

## Description

The **diff** command compares two files and shows the differences between them. In the simplest case, it compares two given files. If "-" is used instead of a file parameter, the content to be compared will come from standard input. The diff command compares text files line by line. If a directory is specified, it will compare files with the same name in those directories, but will not recursively compare subdirectories unless specified.

### Syntax

```shell
diff (options) (parameters)
```

### Options

```shell
-<lines>             Specify how many lines of context to show. This must be used with -c or -u.
-a, --text           Treat all files as text.
-b, --ignore-space-change Ignore changes in the amount of white space.
-B, --ignore-blank-lines  Ignore changes whose lines are all blank.
-c                   Use the context output format.
-C <lines>, --context=<lines> Same as -c with a specified number of lines.
-d, --minimal        Try hard to find a smaller set of changes.
-D <name>, --ifdef=<name> Output merged file with '#ifdef <name>' diffs.
-e, --ed             Output an ed script.
-f, --forward-ed     Output a reversed ed script.
-H, --speed-large-files Use heuristics to speed up comparison of large files.
-I <regexp>, --ignore-matching-lines=<regexp> Ignore changes whose lines all match <regexp>.
-i, --ignore-case    Ignore case differences in file contents.
-l, --paginate       Pass output through 'pr' to paginate it.
-n, --rcs            Output RCS format diffs.
-N, --new-file       Treat absent files as empty.
-p, --show-c-function Show which C function each change is in.
-P, --unidirectional-new-file Treat absent first files as empty.
-q, --brief          Report only whether the files differ.
-r, --recursive      Recursively compare any subdirectories found.
-s, --report-identical-files Report when two files are the same.
-S <file>, --starting-file=<file> Start with <file> when comparing directories.
-t, --expand-tabs    Expand tabs to spaces in output.
-T, --initial-tab    Make tabs line up by prepending a tab.
-u, -U <lines>, --unified=<lines> Output <lines> (default 3) lines of unified context.
-v, --version        Output version information.
-w, --ignore-all-space Ignore all white space.
-W <width>, --width=<width> Output at most <width> (default 130) print columns.
-x <pattern>, --exclude=<pattern> Exclude files that match <pattern>.
-X <file>, --exclude-from=<file> Exclude files that match any pattern in <file>.
-y, --side-by-side   Output in two columns.
--help               Display help.
--left-column        Output only the left column of common lines.
--suppress-common-lines Do not output common lines.
```

### Parameters

* File 1: Specifies the first file to compare.
* File 2: Specifies the second file to compare.

### Examples

#### Compare differences in normal mode

```shell
diff a.txt b.txt
```

#### Compare differences in context mode

```shell
diff -c a.txt b.txt
```

```shell
　　*** a1.txt 2012-08-29 16:45:41.000000000 +0800
　　--- a2.txt 2012-08-29 16:45:51.000000000 +0800
　　***************
　　*** 1,7 ****
　　 a
　　 a
　　 a
　　!a
　　 a
　　 a
　　 a
　　--- 1,7 ----
　　 a
　　 a
　　 a
　　!b
　　 a
　　 a
　　 a
```

#### Compare differences in unified mode

```shell
diff -u a.txt b.txt
```

```shell
　　--- a.txt 2012-08-29 16:45:41.000000000 +0800
　　+++ b.txt 2012-08-29 16:45:51.000000000 +0800
　　@@ -1,7 +1,7 @@
　　 a
　　 a
　　 a
　　-a
　　+b
　　 a
　　 a
　　 a
```

#### Compare differences across multiple files

Compare the file "test.txt" in directory `/usr/li` with "test.txt" in the current directory:

```shell
diff /usr/li test.txt     # Compare files
```

The output will list differences in the specified format:

```shell
n1 a n3,n4  
n1,n2 d n3  
n1,n2 c n3,n4 
```

Where "a", "d", and "c" represent add, delete, and change operations, respectively. "n1" and "n2" represent line numbers in file 1, while "n3" and "n4" represent line numbers in file 2.

Note: The above describes the line numbers and corresponding operations for differences between two files. In the output, affected lines follow each operation. Lines starting with `<` belong to file 1, and lines starting with `>` belong to file 2.
