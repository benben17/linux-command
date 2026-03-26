fgrep
===

Search for fixed-character strings in files.

## Description

The **fgrep command** is used to search the input files specified by the `file` parameter (defaulting to standard input) for lines that match a pattern. The `fgrep` command specifically searches for the `Pattern` parameter, which consists of fixed strings. If more than one file is specified in the `File` parameter, the `fgrep` command will display the file containing the matching line.

The `fgrep` command differs from the `grep` and `egrep` commands because it searches for strings rather than patterns that match expressions. The `fgrep` command uses a fast, compact algorithm. Characters such as `$, *, [, |, (, )` and `\` are interpreted literally by the `fgrep` command. These characters are not interpreted as regular expressions, unlike in the `grep` and `egrep` commands. Because these characters have specific meanings for the shell, the entire string should be enclosed in single quotes `' ... '`. If no file is specified, the `fgrep` command assumes standard input. Generally, each line found is copied to standard output. If there is more than one input file, the filename is printed before each line found.

1. The `fgrep` command is identical to the `grep` command with the `-F` flag, but the error and usage messages differ, and the functionality of the `-s` flag is also different.
2. Each line is limited to 2048 bytes.
3. Paragraphs (under the `-p` flag) are currently limited to a length of 5000 characters.
4. Do not run the `grep` command on special files, as it may produce unpredictable results.
5. Input lines cannot contain null characters.
6. Input files should end with a newline character.
7. Although many flags can be specified simultaneously, some flags will override others. For example, if both `-l` and `-n` are specified, only the filenames will be written to standard output.

### Syntax

```shell
fgrep (options) (parameters)
```

### Options

```shell
-b: Prepend the block number where the line is located to each line found. Using this flag helps find disk block numbers by context. The -b flag cannot be used for standard input or piped input.
-c: Display only the count of matching lines.
-e pattern: Specify the pattern. This mode is simple but useful when the pattern starts with a -(minus sign).
-f StringFile: Specify a file containing the strings.
-h: Hide filenames when multiple files are processed.
-i: Ignore case during comparison.
-l: List only the names of files containing matching lines (once). Filenames are separated by newlines.
-n: Prepend the relative line number of each line in the file.
-pSeparator: Display the entire paragraph containing the matching line. Paragraphs are separated by the paragraph delimiter specified by the Separator parameter, which is a pattern with the same format as the search pattern. Lines containing the paragraph delimiter are used only as delimiters; they are not included in the output. The default paragraph delimiter is a blank line.
-q: Suppress all output to standard output, whether matching or not. If an input line is selected, exit with status 0.
-s: Display only error messages. This is useful for checking the exit status.
-v: Display all lines except those that match the specified pattern.
-w: Perform a word search.
-x: Display lines that match the pattern exactly, with no additional characters.
-y: Ignore case during comparison.
```

This command returns the following exit values:

```shell
0    Match found.
1    No match found.
>1   Syntax error discovered, or file inaccessible (even if a match was found).
```

### Examples

**Search for a simple string in several files:**

```shell
fgrep strcpy *.c
```

Search for the string `strcpy` in all files in the current directory ending with `.c`.

**Count the number of lines matching a pattern:**

```shell
fgrep -c '{' pgm.c
fgrep -c '}' pgm.c
```

Display the number of lines in `pgm.c` that contain a left brace and a right brace.

If no line in your C program contains more than one `{` (left brace) or `}` (right brace), and the braces match correctly, these two numbers will be the same. If the numbers are different, you can display the lines containing the braces in the order they appear in the file using the following command:

```shell
egrep '\{|\}' pgm.c
```

**Display filenames containing a pattern:**

```shell
fgrep -l strcpy *.c
```

Search files ending in `.c` in the current directory and display the filenames that contain the string `strcpy`.
