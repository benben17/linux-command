less
===

Browse file content with screen-by-screen navigation

## Description

The **less** command is very similar to `more`, both used for viewing the content of text files. The difference is that `less` allows the user to navigate both forward and backward through the file, whereas `more` only supports forward navigation. When viewing a file with `less`, use the PageUp key to scroll up and the PageDown key to scroll down. To exit the `less` program, press the Q key.

### Syntax

```shell
less (options) (parameters)
```

### Options

```shell
-e: Automatically exit after the end of the file is reached;
-f: Force opening the file;
-g: Only highlight the current match instead of all occurrences of the search keyword to improve performance;
-I: Ignore case during searches;
-N: Display line numbers at the beginning of each line;
-s: Squeeze consecutive empty lines into a single line;
-S: Display long lines without wrapping;
-x <number>: Set tab stops to the specified number of spaces;
-r: Enable display of raw control characters (allows colorized output).
```

### Parameters

File: Specify the file whose content is to be displayed.

## Examples

```shell
sudo less /var/log/shadowsocks.log

/string: Search downward for "string"
?string: Search upward for "string"
n: Repeat the search in the same direction
N: Repeat the search in the opposite direction
b: Scroll backward one page
d: Scroll forward half a page
u: Scroll backward half a page
y: Scroll backward one line
Q: Exit the less command
Space: Scroll forward one page
Enter: Scroll forward one line
[pagedown]: Scroll forward one page
[pageup]: Scroll backward one page
G: Move to the last line
g: Move to the first line
```
