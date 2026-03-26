expr
===

An expression evaluation tool.

## Description

The **expr command** is an expression evaluation tool used to evaluate expressions and output the results.

Common operators for expr:

- Addition: `+`
- Subtraction: `-`
- Multiplication: `\*`
- Division: `/`
- Modulo (Remainder): `%`

### Syntax

```shell
expr (options) (parameters)
```

### Options

```shell
--help: Display help information for the command.
--version: Display the version information of the command.
```

### Parameters

Expression: The expression to be evaluated.

### Examples

```shell
result=`expr 2 + 3`
result=$(expr $no1 + 5)
```
