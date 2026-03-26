bc
===

An arbitrary precision calculator language.

## Description

The **bc command** is a calculator language that supports arbitrary-precision interactive execution. `bash` built-in support for integer arithmetic exists, but it does not support floating-point operations. The `bc` command can easily perform floating-point calculations, and of course, integer calculations are also supported.

### Syntax

```shell
bc [options] [parameters]
```

### Options

```shell
-i: Force interactive mode.
-l: Define the standard math library to be used.
-w: Give warnings for extensions to POSIX bc.
-q: Do not print the normal GNU bc welcome message.
-v: Display version information.
-h: Display help information.
```

### Parameters

File: Specify a file containing calculation tasks.

### Examples

Advanced arithmetic operations using the `bc` command; it can perform floating-point calculations and some advanced functions:

```shell
echo "1.212*3" | bc 
3.636
```

Set decimal precision (scale):

```shell
echo "scale=2;3/8" | bc
0.37
```

The parameter `scale=2` sets the number of decimal places in the `bc` output to 2.

Base conversion:

```shell
#!/bin/bash
abc=192
echo "obase=2;$abc" | bc
```

The result is `11000000`, which is using `bc` to convert decimal to binary.

```shell
#!/bin/bash
abc=11000000
echo "obase=10;ibase=2;$abc" | bc
```

The result is `192`, which is using `bc` to convert binary to decimal.

Calculate square and square root:

```shell
echo "10^10" | bc
echo "sqrt(100)" | bc
```
