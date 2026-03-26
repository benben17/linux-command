return
===

Exit from a function and return a value.

## Synopsis

```shell
return [n]
```

## Main Purpose

- Causes a shell function to exit and return a value. If the value of `n` is not specified, the default return status is that of the last command executed within the function.

## Parameters

n (optional): An integer.

## Return Value

The return value is the value of the parameter `n` you specified. If the parameter you specify is greater than 255 or less than 0, the return value will always be between 0 and 255 by adding or subtracting 256.

Executing a `return` statement outside of a function will result in a failure.

## Examples

```shell
#!/usr/bin/env bash
# Define a function that returns a value greater than 255
example() {
  return 259
}
# Execute the function
example
# Displays 3 (259 - 256)
echo $?
```

### Note

1. This command is a bash built-in; for related help information, please use the `help` command.
