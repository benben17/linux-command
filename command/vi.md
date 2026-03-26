vi
===

A powerful text editor.

## Description

The **vi command** is the most versatile full-screen plain text editor in UNIX and Unix-like operating systems. The vi editor in Linux is called Vim, which stands for "Vi Improved." It is fully compatible with the vi editor and includes many enhanced features.

The vi editor supports two main modes: Edit mode (Insert mode) and Command mode. Text editing functions are performed in Edit mode, while file operation commands are executed in Command mode. To use the vi editor effectively, you must be proficient in switching between these two modes. By default, opening the vi editor puts you into Command mode. To switch from Edit mode to Command mode, use the "Esc" key. To switch from Command mode to Edit mode, use keys such as "A", "a", "O", "o", "I", or "i".

The vi editor provides a wealth of built-in commands. Some are executed using keyboard combinations, while others require entering a colon ":" followed by the command. Common built-in commands include:

```shell
Ctrl+u: Scroll up half a screen;
Ctrl+d: Scroll down half a screen;
Ctrl+f: Scroll down a full screen;
Ctrl+b: Scroll up a full screen;
Esc: Switch from Edit mode to Command mode;
ZZ: Save changes and exit vi in Command mode;
:line_number: Jump to the beginning of the specified line;
:$: Jump to the beginning of the last line;
x or X: Delete a character (x deletes after the cursor, X deletes before);
D: Delete all characters from the current cursor to the end of the line;
dd: Delete the entire line at the cursor;
ndd: Delete the current line and the following n-1 lines;
nyy: Copy the current line and the following n lines into register '?', where '?' is a letter and n is a number;
p: Paste text below the current cursor position;
P: Paste text above the current cursor position;
/string: Search forward for the specified string from the cursor position;
?string: Search backward for the specified string from the cursor position;
a,bs/F/T: Replace string F with string T between lines a and b (s/ denotes substitution);
a: Append text after the current character;
A: Append text at the end of the line;
i: Insert text before the current character;
I: Insert text at the beginning of the line;
o: Insert a blank line after the current line;
O: Insert a blank line before the current line;
:wq: Save and exit in Command mode;
:w: Save file in Command mode;
:w!: Force save in Command mode;
:q: Exit vi in Command mode;
:q!: Force exit vi without saving;
:e filename: Open and edit the specified file;
:n: Edit the next file if multiple files are open;
:f: Display the current filename, line number, and percentage;
:set number: Display line numbers;
:set nonumber: Hide line numbers;
```

### Syntax

```shell
vi (option) (parameter)
```

### Options

```shell
+<line_number>: Start displaying text from the specified line number;
-b: Open in binary mode, used for editing binary and executable files;
-c<command>: Execute the given command after finishing editing the first file;
-d: Open in diff mode to display differences when multiple files are being edited;
-l: Use Lisp mode, enabling "lisp" and "showmatch";
-m: Disable writing to files by resetting the "write" option;
-M: Disable modifications;
-n: Do not use a swap file;
-o<number>: Specify the number of files to open simultaneously;
-R: Open file in read-only mode;
-s: Quiet mode; do not display error messages for commands.
```

### Parameters

File list: Specifies the list of files to be edited, separated by spaces.

## Extended Knowledge

The vi editor has three operational modes: Command mode, Input (Insert) mode, and ex (Last-line) mode. You can switch between these modes using specific commands or actions.

**Command Mode**

Entering the command `vi` at the shell prompt opens the vi editor in Command mode. In this mode, any characters typed are interpreted as editing commands. For example, `a` (append), `i` (insert), and `x` (delete character). If the input is not a valid vi command, the system may beep, and the cursor will not move. Characters typed in Command mode do not appear on the screen. For instance, typing `i` changes the mode to Input mode without showing any change on the screen.

**Input Mode**

You enter Input mode from Command mode by typing insertion commands such as `i` (insert), `a` (append), `o` (open), `s` (substitute), `c` (change), or `r` (replace). In Input mode, all characters typed are inserted into the buffer as the text of the file and displayed on the screen. Editing commands no longer work in this mode.

To return to Command mode from Input mode, press the `Esc` key. If you are already in Command mode, pressing `Esc` may cause a beep. To ensure you are in Command mode before typing a command, you can press `Esc` several times until you hear a beep or see no change.

**ex Mode**

The vi and ex editors offer the same functionality; the primary difference is the user interface. In vi, commands are usually single letters. In ex, commands are command lines ending with the `Enter` key. vi has a "Last-line" command that allows access to line-oriented ex commands by typing a colon (`:`). The colon appears as a prompt on the status line (usually the bottom line of the screen). You can terminate a command by pressing the interrupt key (usually `Del`). Most file management tasks, such as reading or writing files, are performed in this mode. After an ex command executes, you automatically return to Command mode. For example:

```shell
:1,$s/I/i/g
```

This command replaces all occurrences of uppercase `I` with lowercase `i` from the first line to the end of the file (`$`).

### Displaying Line Numbers
In vi or vim, press `Esc` and then type:
`:set number`
