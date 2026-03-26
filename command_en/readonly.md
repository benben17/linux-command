# readonly

Mark shell variables or functions as read-only.

## Syntax

```shell
readonly [-aAf] [name[=value] ...]
readonly -p
```

## Main Uses

- Define one or more variables and set the read-only attribute.
- Set the read-only attribute for one or more already defined variables.
- Display all variables that have the read-only attribute.
- Set the read-only attribute for one or more already defined functions.
- Display all functions that have the read-only attribute.

## Options

```shell
-a: Refers to indexed arrays.
-A: Refers to associative arrays.
-f: Refers to functions.
-p: Display all read-only variables.
--: Signals the end of options; any further arguments are treated as names.
```

## Parameters

```shell
name (optional): The name of the variable or function.
value (optional): The value to assign to the variable.
```

### Return Value

`readonly` returns true (0) unless an invalid option or an invalid name is provided.

## Examples

```shell
# Define variables and add read-only attribute
readonly var1=13 var2
readonly -a arr1=(1 2 3 4 5) arr2=('z' 'x' 'c')
# The '-A' option is required for associative arrays during definition
readonly -A dict1=(['key1']='value1')
```

```shell
# Define variables and functions first, then add read-only attribute
max=3
readonly max

# Arrays can be defined without `declare -a`
seasons=('spring' 'summer' 'autumn' 'winter')
# The '-a' option is not required when marking an existing array as read-only
readonly seasons

declare -A man=(['age']=23 ['height']='190cm')
# The '-A' option is not required when marking an existing associative array as read-only
readonly man

function foo(){ echo 'bar'; }
# The '-f' option MUST be used to mark a function as read-only
readonly -f foo
```

```shell
# Display all read-only variables; the following two commands produce the same output
readonly
readonly -p
# Display all read-only indexed arrays
readonly -a
# Display all read-only associative arrays
readonly -A
# Display all read-only functions
readonly -f
```

## Common Errors

If a user attempts to modify the value of a read-only variable, an error is reported immediately. For example:

```shell
[root@localhost ~]# readonly test='ok'        # Define and initialize a read-only variable
```

Attempting to modify it:

```shell
[root@localhost ~]# test='my'                 # Attempt to change the value
-bash: test: readonly variable
```

## Notes

1. This is a Bash builtin command; use the `help` command for related information.
2. The `declare +r` command cannot remove the read-only attribute, and `unset` cannot delete read-only variables.
