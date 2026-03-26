dirs
===

Display the directory stack.

## Syntax

```shell
dirs [-clpv] [+N] [-N]
```

## Description

- Display the directory stack.
- Clear the directory stack.

## Options

```shell
-c    Clear the directory stack by deleting all of the entries.
-l    Produce a listing using full pathnames; the default listing format uses a tilde to denote the home directory.
-p    Print the directory stack with one entry per line.
-v    Print the directory stack with one entry per line, prefixing each entry with its index in the stack.
```

## Parameters

+N (Optional): Displays the Nth entry counting from the left of the list printed by `dirs` when invoked without options, starting with zero.

-N (Optional): Displays the Nth entry counting from the right of the list printed by `dirs` when invoked without options, starting with zero.

## Return Value

Returns success unless an invalid option is provided or an error occurs.

## Examples

```shell
# Add directories to the stack.
[user2@pc ~]$ dirs
~
[user2@pc ~]$ pushd -n ~/Desktop
~ ~/Desktop
[user2@pc ~]$ pushd -n ~/Pictures
~ ~/Pictures ~/Desktop
[user2@pc ~]$ pushd -n ~/bin
~ ~/bin ~/Pictures ~/Desktop

# Examples of options and parameters:
[user2@pc ~]$ dirs -l
/home/user2 /home/user2/bin /home/user2/Pictures /home/user2/Desktop
[user2@pc ~]$ dirs -p
~
~/bin
~/Pictures
~/Desktop
[user2@pc ~]$ dirs -v
 0  ~
 1  ~/bin
 2  ~/Pictures
 3  ~/Desktop
[user2@pc ~]$ dirs +2
~/Pictures
[user2@pc ~]$ dirs -2
~/bin
[user2@pc ~]$ dirs -c
[user2@pc ~]$ dirs
~
```

### Notes

1. Bash directory stack commands include `dirs`, `popd`, and `pushd`.
2. The current directory is always at the top of the directory stack.
3. This is a Bash built-in command. For more help, use the `help` command.
