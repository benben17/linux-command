seq
===

Print numbers from a starting number to an ending number with a specified increment.

## Description

The **seq command** is used to generate all integers (or numbers) between one number and another.

### Syntax

```shell
seq [options]... last
seq [options]... first last
seq [options]... first increment last
```

### Options

```shell
-f, --format=FORMAT      Use a printf-style floating-point format.
-s, --separator=STRING   Use the specified string to separate numbers (default: \n).
-w, --equal-width        Pad with leading zeros to make all numbers the same width.
```

### Examples

**-f option: Specify format**

```shell
# seq -f"%3g" 9 11
  9
 10
 11
```

Specified with `%` followed by the number of digits. The default is `%g`. With `%3g`, the part where the number of digits is insufficient is padded with spaces.

```shell
# seq -f"%03g" 9 11
009
010
011
# seq -f"str%03g" 9 11
str009
str010
str011
```

In this case, the part where the number of digits is insufficient is padded with 0. A string can be specified before `%`.

**-w option: Specify equal width for output numbers**

```shell
seq -w 98 101
098
099
100
101
```

Cannot be used with `-f`; the output is equal-width.

**-s option: Specify separator (default is newline)**

```shell
seq -s" " -f"str%03g" 9 11
str009 str010 str011
```

To specify `\t` as the separator:

```shell
seq -s"`echo -e "\t"`" 9 11
```

Specifying `\n` as the separator:

```shell
seq -s"`echo -e "\n"`" 9 11
19293949596979899910911
```

This yields an incorrect result. Generally, there is no need for this as it defaults to a newline as the separator.
