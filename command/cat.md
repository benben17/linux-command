cat
===

Concatenate files and print on the standard output.

## Synopsis

```shell
cat [OPTION]... [FILE]...
```

## Main Purpose

- Display file contents. If no file is specified, or if the file is `-`, read from standard input.
- Concatenate the contents of multiple files and print them to standard output.
- Display non-printing characters (control characters, newlines, tabs, etc.) in the file content.

## Parameters

FILE (optional): The file(s) to be processed. One or more files can be specified.

## Options

```shell
Long options are equivalent to short options.

-A, --show-all           Equivalent to the combined option "-vET".
-b, --number-nonblank    Number non-empty output lines, starting from 1, overriding the "-n" option.
-e                       Equivalent to the combined option "-vE".
-E, --show-ends          Display a '$' character at the end of each line.
-n, --number             Number all output lines, starting from 1.
-s, --squeeze-blank      Suppress repeated empty output lines.
-t                       Equivalent to the combined option "-vT".
-T, --show-tabs          Display TAB characters as "^I".
-u                       POSIX compatibility option, has no effect.
-v, --show-nonprinting   Use "^" and "M-" notation for control characters, except for LFD (line feed, '\n') and TAB.

--help                   Display help information and exit.
--version                Output version information and exit.
```

## Return Value

Returns success unless an invalid option or parameter is provided.

## Examples

```shell
# Concatenate and display multiple files
cat ./1.log ./2.log ./3.log
# Display non-printing characters, tabs, and newlines in a file
cat -A test.log
# Squeeze empty lines in a file
cat -s test.log
# Display a file and append line numbers to the beginning of all lines
cat -n test.log
# Display a file and append line numbers to the beginning of all non-empty lines
cat -b test.log
# Display standard input content together with file content
echo '######' | cat - test.log
```

### Notes

1. This command is part of the `GNU coreutils` package; for related help information, please refer to `man -s 1 cat` or `info coreutils 'cat invocation'`.
2. When using the `cat` command to view **large files**, the text flashes across the screen (scrolling) so quickly that users often cannot see the content. To control the scrolling, press `Ctrl+s` to stop; press `Ctrl+q` to resume; press `Ctrl+c` (interrupt) to terminate the command and return to the shell prompt.
3. It is recommended to use `less`, `more`, or text editors like `emacs` or `vi` when viewing **large files**.

### Reference Links

1. [Question about LFD key](https://superuser.com/questions/328054/is-there-an-lfd-key-on-my-keyboard)
