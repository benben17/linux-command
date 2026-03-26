local
===

Define local variables within a function.

## Synopsis

```shell
local [-aAfFgilnrtux] [-p] [name[=value] ...]
```

## Main Purpose

- Define local variables within a function.
- Display local variables.
- Define global variables within a function (depending on attributes).

## Options

The options for `local` are the same as those for `declare`; please refer to the `declare` command for details.

## Parameters

name (optional): Variable name or defined function name.
value (optional): The value to assign to the variable.

## Return Value

`local` returns true unless an invalid option is provided, an assignment error occurs, or the command is used outside of a function.

## Examples

Please refer to the `declare` command for relevant examples.

## Incorrect Usage

- Using this command outside of a function.

### Notes

1. This command is a Bash built-in; refer to the `help` command or the Bash manual (`man bash`, `info bash`) for more information.
