unset
===

Remove specified shell variables or functions.

## Synopsis

```shell
unset [-f] [-v] [-n] [name ...]
```

## Main Uses

- Remove one or more shell variables (excluding read-only variables).
- Remove one or more shell functions.
- Remove one or more variables with the nameref attribute (if the -n option is present).

## Options

```shell
-f: Remove functions only.
-v: Remove variables only (excluding read-only variables).
-n: Remove the variable name with the nameref attribute (if the option exists).
```

## Parameters

name (optional): The variable or function to be removed.

## Return Value

Returns success unless an option is invalid or the variable/function to be removed has the read-only attribute.

## Examples

```shell
# Remove a variable.
declare paper_size='B5'
unset -v paper_size
```
```shell
# Remove a function.
function show_result(){ echo "Last Command Return: $?"; }
unset -f show_result
```
```shell
# When no options are specified, variables are prioritized; if that fails, functions are removed.
declare -i aa=100
function aa(){ echo 'aa'; }
unset aa
# Variable 'aa' has been removed.
declare -p aa
# Function 'aa' still exists.
declare -F | grep aa
```
```shell
# Demonstrating unset with the -n option when name specifies a reference variable.
declare a=3
# Define a reference variable
declare -n b=a
# Check attributes; shows declare -n b="a"
declare -p b
# Displays 3
echo ${b}
# Displays a
echo ${!b}
# When the -n option is specified
unset -n b
# Reference variable b has been removed
declare -p b
# Referenced variable a has not been removed
declare -p a
```

```shell
# Demonstrating unset without the -n option when name specifies a reference variable.
declare a=3
# Define a reference variable
declare -n b=a
# Check attributes; shows declare -n b="a"
declare -p b
# Displays 3
echo ${b}
# Displays a
echo ${!b}
# When the -n option is not specified
unset b
# Reference variable b is not removed; shows declare -n b="a"
declare -p b
# Referenced variable a is removed
declare -p a
```

### Note

1. This is a Bash built-in command. For related help information, please use the `help` command.
