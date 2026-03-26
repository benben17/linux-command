xclip
===

Command line interface to the X11 clipboard

## Description

In the X Window System, there are two primary mechanisms for copying text between windows: **Selections** and **cut buffers**.

The standard "copy & paste" typically uses cut buffers or the `CLIPBOARD` selection. However, selecting text with the mouse and then middle-clicking in another window uses the `PRIMARY` selection mechanism.

When you select text with the mouse, it is automatically copied to the `PRIMARY` selection. Middle-clicking then pastes the content of this selection.

While these methods are convenient for small snippets, they can be cumbersome for large blocks of text or repetitive tasks. **xclip** provides a convenient command-line interface to manage X selections and clipboards.

For example, the following command copies the content of `/etc/passwd` to the `PRIMARY` selection:

```shell
xclip -i /etc/passwd
```

You can then paste it anywhere using the middle mouse button or `Shift+Insert`.

A common use case is to bind `xclip` commands to keyboard shortcuts. For instance, you could bind `Alt+F1` to copy the content of `~/snippet1.txt` to the clipboard, and `Alt+F2` for `~/snippet2.txt`. This allows for efficient copying of frequently used strings, such as passwords or code snippets.

### Syntax

```shell
xclip [options] [file]
```

### Common Options

- `-i, -in`: Read text into X selection from standard input (default).
- `-o, -out`: Print X selection to standard output.
- `-selection <name>`: Specify which X selection to use (`primary`, `secondary`, or `clipboard`). Default is `primary`.
- `-loops <count>`: Number of X selection requests to service before exiting.
- `-display <display>`: Specify the X server to connect to.
- `-h, -help`: Display help information.
