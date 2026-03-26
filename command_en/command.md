command
===

Call and execute a specified command

## Description

The **command command** calls and executes a specified instruction. When the command is executed, shell functions are not searched. The `command` command can only execute shell built-in commands or external commands, bypassing functions with the same name.

### Syntax

```shell
command [arguments]
```

### Arguments

Instruction: The command and its arguments to be called.

### Examples

Use the `command` command to call and execute `echo Linux`:

```shell
command echo Linux            # Call and execute a shell built-in instruction
```

After executing the above command, `echo Linux` will be called and executed, with the following result:

```shell
Linux
```
