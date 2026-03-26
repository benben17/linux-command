echo
===

Display a line of text or variable values.

## Description

The **echo** command is used to print the value of shell variables or directly output specified strings. The Linux **echo** command is extremely common in shell programming and terminal usage. Its primary function is to display a piece of text on the monitor, often serving as a prompt.

### Syntax

```shell
echo [OPTION] [STRING]
```

### Options

```shell
-e: Enable interpretation of backslash escapes.
-E: Disable interpretation of backslash escapes (default).
-n: Do not output the trailing newline.
```

When using the `-e` option, the following sequences are recognized:

- `\a` alert (bell);
- `\b` backspace;
- `\c` produce no further output;
- `\f` form feed;
- `\n` new line;
- `\r` carriage return;
- `\t` horizontal tab;
- `\v` vertical tab;
- `\\` backslash;
- `\nnn` the character whose ASCII code is the octal value nnn.

### Parameters

Variable: Specify the variable or string to be printed.

### Examples

```shell
/bin/echo Hello, world!
```

In the above command, two words (Hello and world!) are passed as separate arguments to echo, and echo prints them in order, separated by a space.

The following command produces the same output:

```shell
/bin/echo 'Hello, World!'
```

Unlike the first example, the above command provides the single-quoted string 'Hello, world!' as a single argument. Single quotes protect it from shell interpretation, passing special characters and escape sequences literally to echo.

For example, in the `bash shell`, variable names are prefixed with a dollar sign ($). In the next command, the variable name inside quotes is treated literally, while outside quotes, it is expanded to its value.

```shell
/bin/echo 'The value of $PATH is' $PATH
# The value of $PATH is
# /home/hope/bin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Printing colored text with the `echo` command:

**Text Color:**

```shell
echo -e "\e[1;31mThis is red text\e[0m"
This is red text
```

*   `\e[1;31m` sets the color to red.
*   `\e[0m` resets the color.

Color codes: Reset=0, Black=30, Red=31, Green=32, Yellow=33, Blue=34, Magenta=35, Cyan=36, White=37.

```shell
echo -e "\x1b[30;1m 0 Black \x1b[0m"\
"\x1b[31;1m 1 Red \x1b[0m"\
"\x1b[32;1m 2 Green \x1b[0m"\
"\x1b[33;1m 3 Yellow \x1b[0m"\
"\x1b[34;1m 4 Blue \x1b[0m"\
"\x1b[35;1m 5 Magenta \x1b[0m"\
"\x1b[36;1m 6 Cyan \x1b[0m"\
"\x1b[37;1m 7 White \x1b[0m"
```

**Background Color:**

```shell
echo -e "\e[1;42mGreen Background\e[0m"
Green Background
```

Color codes: Reset=0, Black=40, Red=41, Green=42, Yellow=43, Blue=44, Magenta=45, Cyan=46, White=47.

**Flashing Text:**

```shell
echo -e "\033[37;31;5mMySQL Server Stop...\033[39;49;0m"
```

Other parameters for the numeric position: 0 (Reset), 1 (Bold), 4 (Underline), 5 (Flash), 7 (Reverse), 8 (Conceal).

**Output without trailing newline:**

```shell
echo -n 'hello'
```
