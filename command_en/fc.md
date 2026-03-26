fc
===

Display commands from the history list or modify and execute specified history commands.

## Synopsis

```shell
fc [-e ename] [-lnr] [first] [last]
fc -s [pat=rep] [command]
```

## Main Purpose

- Display commands from the history list.

- Edit and re-execute commands from the history list.

## Options

```shell
-e ename                  Select the editor to use. The default calling order is the environment variable `FCEDIT`, then `EDITOR`, and finally `vi`.
-l                        List the commands instead of editing them.
-n                        Do not output line numbers when listing (must be used with the -l option).
-r                        List commands in reverse order, with the most recently executed first (must be used with the -l option).
-s [pat=rep] [command]    The command (defaults to the last executed command if not specified) will be re-executed after replacing `pat` with `rep`.
```

## Parameters

first: Optional; can be a string (the most recent command starting with that string), a number (index in the history list, negative numbers represent an offset from the current command number). If not specified, it defaults to the previous command with an offset of -16 (the 16 most recent commands).

last: Optional; can be a string (the most recent command starting with that string), a number (index in the history list, negative numbers represent an offset from the current command number). If not specified, it defaults to the value of the `first` parameter.

## Return Value

Returns success or the status of the executed command. Returns a non-zero value when an error occurs.

## Examples

Replace command parameters:

```shell
# List the ~ directory
ls ~
# Replace ~ with /; after replacement, list the root directory.
fc -s ~=/
```

Display the 10 most recently used history commands:

```shell
[root@localhost ~]# fc -l -10
1039     type -a grep
1040     export
1041     history 10
1042     ulimit -a
1043     shopt
1044     help ls
1045     help env
1046     help short
1047     help shopt
1048     showkey -a
```

Edit history command number 1040:

```shell
[root@localhost ~]# fc 1040
```

### Note

1. After closing the terminal, the history list will be written to the history file `~/.bash_history`.
2. The value of the environment variable `FCEDIT` is the default editor for `fc`.
3. This command is a bash built-in; for related help information, please refer to the `help` command.
