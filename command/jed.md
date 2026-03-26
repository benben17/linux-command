jed
===

A powerful text editor for programmers.

## Description

The `jed` editor, developed using the S-Lang library, is primarily used for editing program source code. It supports syntax highlighting and can emulate editors like Emacs, EDT, WordStar, and Brief.

### Syntax

```shell
jed [options] [files]
```

### Options

```shell
-2 : Display two editing areas (split screen).
-batch : Run in batch mode.
-f <func> : Execute an S-Lang function.
-g <line> : Go to a specific line number.
-i <file> : Load a file into a buffer.
-n : Do not load the `jed.rc` configuration file.
-s <str> : Search for and move to a specific string.
```

### Parameters

Files: A list of files to be edited.

### Examples

Open a C source file with a split screen view:
```shell
jed -2 mysource.c
```

#### Configuration

- `/usr/share/jed/lib/*.sl`: Default JED S-Lang files.
- `/usr/share/jed/lib/site.sl`: Default startup file.
- `/etc/jed.rc`: Global system configuration.
- `~/.jedrc`: User configuration file.

`jed` can emulate several editors; by default, it often uses Emacs keybindings. Use F10 to access the menu.
