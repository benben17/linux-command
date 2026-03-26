history
===

Display or manipulate the history list.

## Synopsis

```shell
history [-c] [-d offset] [n]
history -anrw [filename]
history -ps arg [arg...]
```

## Description

- Displays the history list of commands.
- Manipulates the command history.

## Options

```shell
-c           # Clear the history list.
-d offset    # Delete the history entry at position offset. If offset is positive, it specifies the position; if negative, it specifies the position relative to the end.
-a           # Append the current session's history entries to the history file.
-n           # Append history entries not yet read from the history file to the current history list.
-r           # Read the history file and append its contents to the history list.
-w           # Write the current history list to the history file.
-p           # Perform history expansion on each argument and display the result on standard output, without storing it in the history list.
-s           # Append each argument as a single entry to the history list.
```

## Parameters

n: Optional. List only the most recent n entries.

filename: Optional. The history file to use. The default order is `filename`, the `HISTFILE` environment variable, or `~/.bash_history`.

## Return Value

Returns success unless an invalid option is provided or an error occurs.

## Examples

Display the last 5 history commands:

```shell
[root@localhost ~]# history 5
   97  cd .ssh/
   98  ls
   99  cat known_hosts
  100  exit
  101  history 10
```

Clear the history:

```shell
[root@localhost ~]# history -c
```

Delete a specific line:

```shell
[root@localhost ~]# history -d 2243
```

Quickly execute a history command:

```shell
# Execute the nth command in history
[root@localhost ~]# !n

# Execute the last command starting with 'xxx'
[root@localhost ~]# !xxx
```

### Note

1. In the command line, you can use `!` followed by a number to execute the corresponding command from history. For example, `!2` executes the second command.
2. When the terminal is closed, the history list is written to `~/.bash_history`.
3. The `HISTSIZE` environment variable determines the number of commands stored in the history file (default is 1000).
4. If the `HISTTIMEFORMAT` environment variable is set, its value is used as a format string for `strftime(3)` to print a timestamp before each history entry.
5. This command is a bash built-in. Use `help history` for more information.
