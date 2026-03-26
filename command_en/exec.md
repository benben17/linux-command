exec
===

Invoke and execute a specified command.

## Description

The **exec** command is used to invoke and execute a command. It is commonly used in shell scripts to call other commands. If used directly in the current terminal, the terminal will exit immediately after the specified command finishes executing.

### Syntax

```shell
exec [options] [parameters]
```

### Options

```shell
-c: Execute the specified command in an empty environment.
```

### Parameters

Command: The command to be executed along with its arguments.

### Examples

First, use the `echo` command to output the text "Linux C++":

```shell
echo Linux C++           # Output specified information
```

Output:

```shell
Linux C++                # Output information
```

Then use the `exec` command to call `echo` to output the same information:

```shell
exec -c echo Linux C++          # Invoke command
```

Output:

```shell
Linux C++                       # Output information using specified command
```

Comparing the results, the functionality achieved is the same, indicating that the `exec` command successfully called the `echo` command.
