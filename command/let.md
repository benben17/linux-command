let
===

A simple calculator for performing arithmetic expressions.

## Synopsis

```shell
let arg [arg ...]
```

## Main Purpose

- Execute one or more arithmetic expressions.

## Parameters

arg: Arithmetic expression

## Return Value

Returns `1` if the result of the last expression evaluated by `let` is 0; otherwise returns `0`.
Returns `1` and an error message if an expression executed by `let` involves division by zero.

## Operator Precedence (Descending Order)

| **Operator** | **Description** |
|:-------:|:-------:|
| `id++, id--` | Variable post-increment, post-decrement |
| `++id, --id` | Variable pre-increment, pre-decrement |
| `-, +` | Unary minus, unary plus |
| `!, ~` | Logical negation, bitwise negation |
| `**` | Exponentiation |
| `*, /, %` | Multiplication, division, modulo |
| `+, -` | Addition, subtraction |
| `<<, >>` | Bitwise left shift, right shift |
| `<=, >=, <, >` | Comparison |
| `==, !=` | Equality, inequality |
| `&` | Bitwise AND |
| `^` | Bitwise XOR |
| `|` | Bitwise OR |
| `&&` | Logical AND |
| `||` | Logical OR |
| `expr ? expr : expr` | Conditional (ternary) operator |
| `=, *=, /=, %=, +=, -=,` <br> `<<=, >>=, &=, ^=, |=` | Assignment |

## Examples

```shell
# Attempting to execute an arithmetic expression directly in the terminal (like Python IDLE).
3+4
bash: 3+4: command not found...
# Trying another way.
3 + 4
bash: 3: command not found...
# It seems it doesn't work directly.
```

```shell
# Using the let command for assignment.
let a=3**4
echo ${a}
# Output: 81
# ((...)) is equivalent to the let command.
((a=3**4))
```

```shell
# let is commonly used for variable assignment, while the external command expr can directly return the value of an expression.
let 3+4
# No output (7 is not displayed).
# This outputs 7; note the spaces.
expr 3 + 4
```

```shell
# Conditional expressions.
if ((8>4)); then
  echo '8 is greater than 4.'
else
  echo 'error'
fi
# Note the spaces in the [[]] form.
if [[ 12 -le 10 ]]; then
  echo 'error'
else
  echo '12 is greater than 10.'
fi
```

```shell
# Arithmetic operations can be performed by setting the integer attribute with the declare command.
# The local command works similarly.

# Integer attribute not specified; the output is the string 'a+b'.
declare a=3 b=4 c
c=a+b
echo ${c}
# However, you can assign it like this:
c=$((a+b))
echo ${c}
# Output: 7

# With the integer attribute set, you can perform addition directly.
declare -i a=3 b=4 c
c=a+b
echo ${c}
# Same as above.
declare -i a
a=2*3
echo ${a}
# Output: 6
```

### Notes

1. This command is a Bash built-in; use the `help` command for more information.
2. In addition to `let`, other commands for arithmetic calculation include external commands like `expr` and `bc`.
