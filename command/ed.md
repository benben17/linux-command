ed
===

Line-oriented text editor.

## Description

The **ed** command is a line-oriented text editor. It has two working modes: command mode and input mode. The `ed` command supports several built-in commands. Common built-in commands are as follows:

### Syntax

```shell
ed [options] [parameters]
```

### Options

**Common commands within ed:**

```shell
A # Switch to input mode and append new content after the last line of the file.
C # Switch to input mode and replace the last line with the input content.
i # Switch to input mode and insert a new blank line before the current line.
d # Delete the last line of text.
n # Display the line number and content of the last line.
w <filename> # Save the currently edited file with the given filename.
q # Quit the ed editor.
```

**CLI Options:**

```shell
-G, --traditional: Provide compatible features.
-p <string>: Specify the prompt character for command mode.
-s, -, --quiet, --silent: Suppress diagnostic messages when opening files.
--help: Display help.
--version: Display version information.
```

### Parameters

File: The file to be edited.
