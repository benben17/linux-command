more
===

Display file content, one screen at a time

## Description

The **more command** is a text filter based on the `vi` editor for paging through text files. It displays the content of a text file one screen at a time and supports basic `vi`-like navigation. It has several built-in shortcut keys, commonly including H (help), Enter (scroll down one line), Space (scroll down one screen), and Q (exit).

This command displays one screen of text at a time. After a full screen, it pauses and displays a prompt at the bottom of the screen, showing the percentage of the file displayed so far: `--More-- (XX%)`. You can respond to the prompt in several ways:

*   Press `Space`: Display the next screen of text.
*   Press `Enter`: Display the next line of text.
*   Press slash `/`: Followed by a pattern to search for the next occurrence in the text.
*   Press `H`: Display the help screen with related information.
*   Press `B`: Display the previous screen of text.
*   Press `Q`: Exit the `more` command.

### Syntax

```shell
more [options] [file]
```

### Options

```shell
-<number>: Specify the number of lines to display per screen.
-d: Display "[press space to continue, 'q' to quit.]" and "[Press 'h' for instructions]".
-c: Do not scroll. Instead, clear the screen and then display the text.
-s: Squeeze multiple blank lines into one.
-u: Suppress underlining.
+<number>: Start displaying from the specified line number.
```

### Parameters

File: Specifies the file to be displayed page by page.

### Examples

Display the content of `file`, clearing the screen before displaying and showing the completion percentage at the bottom.

```shell
more -dc file
```

Display the content of `file` 10 lines at a time, clearing the screen before each display.

```shell
more -c -10 file
```
