emacs
===

Powerful full-screen text editor.

## Description

The **emacs** command is a powerful full-screen text editor developed by Richard Stallman, the founder of the GNU project. It supports multiple programming languages and has many excellent features. It is widely used by system administrators and software developers.

### Syntax

```shell
emacs [options] [parameters]
```

### Options

```shell
+<line_number>: Start emacs and move the cursor to the specified line number.
-q: Start emacs without loading the initialization file.
-u <user>: Load the initialization file of the specified user.
-t <file>: Use the specified file as a terminal, instead of using standard input (stdin) and standard output (stdout).
-f <function>: Execute the specified Lisp function.
-l <lisp_file>: Load the specified Lisp code file.
-batch: Run emacs in batch mode.
```

### Parameters

File: Specify the text file to be edited.

## Emacs Command Reference

### Basic Commands

```shell
C-x C-c : Exit Emacs
C-x C-f : Open a file; if it doesn't exist, create it.
C-g : Cancel a partially entered command.
```

### Editing

```shell
C-z (redefined): Undo; originally C-z was to suspend Emacs (use 'fg' to resume). C-x u is the default undo. Move the cursor and C-z again to redo.
M-d : Delete the word after the cursor.
```

### Moving the Cursor

```shell
C-v : Page forward
M-v : Page backward
M-r : Move cursor to the middle line of the screen.
C-a : Move to the beginning of the line.
M-a : Move to the beginning of the sentence (there may be spaces between the line start and sentence start).
C-e : Move to the end of the line.
M-e : Move to the end of the sentence.
M-{ : Move up one paragraph.
M-} : Move down one paragraph.
C-right : Move forward one word.
C-left : Move backward one word.
C-up : Move up one paragraph.
C-down : Move down one paragraph.
M-< : Move to the beginning of the buffer.
M-> : Move to the end of the buffer.
C-u <number> <command> : Execute the command multiple times (number of times). "M-<number> <command>" also works.
M-x goto-line : Move to a specific line.
C-l : Redraw screen, centering the current line in the window.
```

### Buffer Related

```shell
C-x k : Kill current buffer.
C-x b : Switch to the previous buffer.
C-x C-b : List all buffers.
C-x C-s : Save current buffer.
C-x s : Save all modified buffers (prompts for each).
C-x C-w : Save file as.
```

### Copy and Paste

```shell
M-space (redefined): Set mark; C-@ is the default.
C-w (redefined) : Kill (cut) region; if no mark is set, kill the current line.
M-w (redefined) : Copy region; if no mark is set, copy the current line.
C-k : Kill from cursor to end of line.
C-y : Yank (paste).
M-y : Cycle through previous kills after C-y.
C-x r k : Kill rectangular region.
C-x r y : Yank rectangular region.
```

### Window Operations

```shell
C-x 0 : Close current window.
C-x 1 : Maximize current window.
C-x 2 : Split window vertically.
C-x 3 : Split window horizontally.
M-o (redefined) : Switch between windows; C-x o is the default.
C-x 5 1/2/3/0 : Similar operations for frames.
C-x < : Scroll window content right.
C-x > : Scroll window content left.
(C-u) C-x ^ : Increase window height.
(C-u) C-x } : Increase window width.
(C-u) C-x { : Decrease window width.
ESC C-v : Scroll other window.
```

### Search and Replace

```shell
C-s : Incremental search forward; press C-s again for next occurrence.
C-s RET : Normal search.
C-r : Incremental search backward.
C-s RET C-w : Search by word.
M-% : Query replace (asks before each replacement).
M-x replace-string : Simple replace string.
```

### Tags

```shell
M-! etags *.c *.h : Create TAGS file.
M-. : Jump to tag definition.
M-x list-tags : List tags.
```

### Bookmarks

```shell
C-x r m : Set bookmark.
C-x r b : Jump to bookmark.
```

### Help

```shell
C-h ? : View help information.
C-h f : Describe a function.
C-h v : Describe a variable.
C-h k : Describe a key binding.
C-h C-f : View info for a function.
C-h i : View Info manuals.
```

### Other

```shell
C-M-\ : Indent region according to major mode.
C-x h : Select all.
M-! : Execute external shell command.
M-x shell : Run a shell in a buffer.
M-x term : Run a terminal emulator.
C-x C-q : Toggle read-only mode for buffer.
```
