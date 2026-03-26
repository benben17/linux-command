dc
===

An arbitrary-precision calculator

## Description

**dc** is a reverse-Polish desk calculator which supports unlimited precision arithmetic. It also allows you to define and call macros. Normally dc reads from the standard input, but it can also read from files passed as arguments.

## Syntax

```shell
dc [options] [file...]
```

### Options

```shell
-e, --expression=EXPR    # Evaluate expression
-f, --file=FILE          # Evaluate file content
-h, --help               # Display help and exit
-V, --version            # Output version information and exit
```

### Commands

```shell
p  Prints the value on the top of the stack, with a newline.
n  Prints the value on the top of the stack and pops it, without a newline.
f  Prints the entire contents of the stack without altering anything.
P  Pops the value off the top of the stack.
c  Clears the stack.
d  Duplicates the value on the top of the stack, pushing the copy onto the stack.
r  Reverses the order of the top two elements on the stack.
Z  Pops a value off the stack, calculates its number of digits, and pushes that number.
X  Pops a value off the stack, calculates its number of fractional digits, and pushes that number.
z  Pushes the current stack depth onto the stack.
i  Pops a value off the stack and uses it as the input radix.
o  Pops a value off the stack and uses it as the output radix.
k  Pops a value off the stack and uses it to set the precision.
I  Pushes the value of the input radix onto the stack.
O  Pushes the value of the output radix onto the stack.
K  Pushes the current precision onto the stack.
```

## Examples

The following example shows how to calculate `10 * 10` using `dc`:

```shell
$ dc

10          # 1. Input number 10
10          # 2. Input number 10
*           # 3. Input '*' for multiplication
p           # 4. Input 'p' to print the result
100
q           # 5. Input 'q' to quit dc
```

Example showing a calculation from the command line resulting in `509`:

```bash
$ dc --expression="50 10 * 9 + p"
509
```

## Supported Operations

`+` Pops two values, adds them, and pushes the result.

`-` Pops two values, subtracts the first popped value from the second popped value, and pushes the result.

`*` Pops two values, multiplies them, and pushes the result. The number of fractional digits in the result depends on the current precision and the number of fractional digits in the two arguments.

`/` Pops two values, divides the second popped value by the first popped value, and pushes the result. The number of fractional digits is specified by the precision value.

`%` Pops two values, computes the remainder of the division that the `/` command would perform, and pushes that value.

`~` Pops two values and divides the second popped value by the first. The quotient is pushed first, followed by the remainder. The number of fractional digits used in the division is specified by the precision.

`^` Pops two values and performs exponentiation, using the first popped value as the exponent and the second as the base. Any fractional part of the exponent is ignored.

`|` Pops three values and computes modular exponentiation. The first popped value is used as the modulus (must be a non-zero integer). The second is the exponent (must be a non-negative integer). The third is the base.

`v` Pops one value, computes its square root, and pushes the result. The number of fractional digits in the result is determined by the current precision and the precision of the argument.
