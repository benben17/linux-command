shift
===

Shift positional parameters.

## Synopsis

```shell
shift [n]
```

## Main Description

- Renames the positional parameters `$n, $n+1...` to `$1, $2...`.

## Parameters

n (optional): An integer greater than or equal to 1 and less than or equal to the number of parameters, defaulting to 1.

## Return Value

Returns success unless n is greater than the number of parameters or n is less than 1, or other illegal values.

## Examples

Suppose our script file (test.sh) is as follows:

```shell
#!/usr/bin/env bash
# Display the first three positional parameters.
echo "$1 $2 $3"
# Remove the first two positional parameters, rename $3 to $1, and so on.
shift 2
echo "$1 $2 $3"
```

Execute the script in the terminal:

```shell
sh test.sh q w e r t
```

The output is as follows:

```shell
q w e
e r t
```

### Note

1. This command is a bash built-in; for related help information, please check the `help` command.
