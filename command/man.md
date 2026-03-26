man
===

Display reference manuals for Linux commands

## Description

The **man command** is the primary interface used to read the system's reference manuals (man pages). These pages provide detailed information about commands, configuration files, system calls, and library functions.

### Syntax

```shell
man [OPTION]... [SECTION] PAGE...
```

### Options

```shell
-a：Search all manual sections for the specified keyword.
-f：Equivalent to the `whatis` command; display a short description of the keyword.
-P <pager>：Specify the pager to use for displaying output (e.g., `less`).
-M <path>：Specify the search path for manual pages.
```

### Parameters

*   Section: The manual section to search in (see below).
*   Keyword/Page: The name of the command or function to look up.

### Manual Sections

Manual pages are organized into sections:

```shell
1：Executable programs or shell commands.
2：System calls (functions provided by the kernel).
3：Library calls (functions within program libraries, e.g., libc).
4：Special files (usually found in /dev).
5：File formats and conventions (e.g., /etc/passwd).
6：Games.
7：Miscellaneous (including macro packages and conventions, e.g., man(7), ascii(7)).
8：System administration commands (usually only for root).
9：Kernel routines (non-standard).
```

### Examples

Running `man ls` will show "LS(1)" in the top corner, indicating that `ls` is in Section 1 (User Commands). Running `man ifconfig` will show "IFCONFIG(8)", indicating Section 8 (System Administration).

`man` searches sections in numerical order. For example:

```shell
man sleep
```

This usually displays the `sleep` command (Section 1). To view the `sleep` library function, specify Section 3:

```shell
man 3 sleep
```

### Related Commands

* `tldr`: A simplified, community-driven manual that provides practical examples instead of exhaustive documentation.
  * Repository: [https://github.com/tldr-pages/tldr/](https://github.com/tldr-pages/tldr/)
  * Official Site: [https://tldr.sh/](https://tldr.sh/)
  * Online Version: [https://tldr.ostera.io/](https://tldr.ostera.io/)
