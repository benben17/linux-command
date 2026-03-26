pico
===

A simple, display-oriented text editor.

## Description

**pico** is a simple, easy-to-use, full-screen text editor. It provides a variety of keyboard shortcuts displayed at the bottom of the screen.

Common shortcuts:
*   `Ctrl+G`: Get help.
*   `Ctrl+O`: Save (Write Out) the file.
*   `Ctrl+R`: Read a file into the current one at the cursor position.
*   `Ctrl+Y`: Page Up.
*   `Ctrl+V`: Page Down.
*   `Ctrl+W`: Search (Where Is) for text.
*   `Ctrl+K`: Cut the current line.
*   `Ctrl+U`: Uncut (Paste) the last cut text.
*   `Ctrl+C`: Show current cursor position.
*   `Ctrl+T`: Spell check the document.
*   `Ctrl+J`: Justify the current paragraph.
*   `Ctrl+X`: Exit (prompts to save if modified).

### Syntax

```shell
pico [options] [file]
```

### Options

```shell
-b: Enable search and replace.
-d: Enable the delete key to work correctly.
-e: Use full filenames.
-f: Enable function keys (F1, F2, etc.).
-g: Show the cursor in the file browser.
-h: Display help.
-k: Cut from cursor to end of line instead of the whole line.
-m: Enable mouse support.
-n <interval>: Set the interval (in seconds) for checking new mail.
-o <dir>: Set the operating directory.
-r <width>: Set the editing fill column width.
-v: View mode (read-only).
-w: Disable automatic word wrap.
-x: Disable the shortcut menu at the bottom.
-z: Enable suspension (Ctrl+Z).
+<line>: Start at the specified line number.
```

### Parameters

File: The file to be edited.
