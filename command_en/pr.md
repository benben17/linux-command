pr
===

Convert text files for printing

## Description

The **pr command** is used to convert text files into a format suitable for printing. It can split large files into multiple pages for printing and add a title to each page.

### Syntax

```shell
pr(options)(parameters)
```

### Options

```shell
-e<tab[width]> (--expand-tabs=<tab[width]>): Expand tabs (or tab characters) to spaces. If width is specified, convert tabs to that width; otherwise, the default is 8.
-h<title>: Specify a title for the page header.
-i<out-tab-char[out-tab-width]> (--output-tabs<out-tab-char[out-tab-width]>): Replace spaces with tabs in output. You can specify an alternative tab character (default is tab) and width (default is 8).
-l<lines>: Specify the number of lines per page.
-n<separator[digits]>: Number columns, or use the -m option to number lines. Append a separator to each number (default is tab) and limit the number of digits (default is 5).
-o<width>: Set the width for the left margin.
-s<separator> (--separator<separator>): Use the specified separator (default is tab) instead of spaces to separate columns.
-S<string> (--sep-string<string>): Use the specified string (default is tab for -J) or a space to separate columns.
-w<page_width>: Set page width for multi-column output (default is 72).
-W<page_width>: Set page width to a fixed value (default is 72).
-J (--join-lines): Join full lines, ignoring -W if set.
-num_cols: num_cols is an integer; specify the number of columns to print for a file.
-m (--merge): Print all files, one per column.
-f (-F) (--form-feed): Use form feeds instead of newlines.
-r (--no-file-warnings): Silent when an input file cannot be opened.
-t: Omit page headers and footers.
-T (--omit-pagination): Similar to -t, but also omit form feeds.
-v (--show-non-printing): Convert non-printing characters to octal backslash notation.
-d: Double space the output.
-a (--across): Print columns across (horizontally) rather than down.
-c (--show-control-chars): Convert control characters to hat notation (e.g., ^C) and other non-printing characters to octal backslash notation.
--help: Print help information and exit.
--version: Print version information and exit.
```

### Parameters

File: The files to be converted.
