info
===

Read documentation in Info format.

## Description

The `info` command is a tool for viewing help documentation in the Info format on Linux.

Info pages are generally better written, easier to understand, and more friendly than man pages, although man pages are often quicker to use. While a man page is typically a single page, Info pages are organized into multiple sections (called nodes), which can contain subsections (sub-nodes). The key to using this command is learning how to navigate within a page and how to switch between nodes and sub-nodes. It might be challenging at first to move between nodes, which is ironic given that it was intended to be easier for beginners than the `man` command.

### Syntax

```shell
info [options] [topic]
```

### Options

```shell
-d : Add a directory to the Info search path.
-f : Specify the Info file to read.
-n : Specify the node in the first visited Info file.
-o : Output selected nodes to a file.
```

### Parameters

Topic: The subject to get help on (command, function, or configuration file).

### Examples

View the Info documentation for the `info` command itself:

```shell
info info
```

#### Common Shortcuts

- `?`: Show a summary of common shortcuts.
- `n`: Move to the "Next" node at this level.
- `p`: Move to the "Previous" node at this level.
- `u`: Move "Up" to the parent of this node.
- `m`: Follow a menu item (type the name and press Enter).
- `g`: Go to a specific node by name.
- `l`: Return to the "Last" visited node.
- `SPACE`: Scroll forward one page.
- `BACKUP` or `DEL`: Scroll backward one page.
- `q`: Quit `info`.

#### Interactive Commands

- `Ctrl-x 0`: Close the help window.
- `Ctrl-x Ctrl-c`: Exit Info.
- `b`, `t`, or `Home`: Go to the beginning of the document.
- `e` or `End`: Go to the end of the document.
- `Ctrl-l`: Redraw the screen.
- `Ctrl-g`: Cancel the current command.
