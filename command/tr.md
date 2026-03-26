tr
===

Translate, squeeze, and/or delete characters

## Description

The **tr command** is used to translate, squeeze, or delete characters from standard input. it can transform one set of characters into another and is frequently used to write elegant, powerful one-liners.

### Syntax

```shell
tr [options] [parameters]
```

### Options

```shell
-c, --complement: Replace all characters not in the first character set;
-d, --delete: Delete all characters in the first character set;
-s, --squeeze-repeats: Replace sequences of repeated characters with a single instance of that character;
-t, --truncate-set1: Truncate the first set to the length of the second set before translation.
```

### Parameters

*   Set1: Specifies the original character set to be translated or deleted. When performing translation, Set2 must be specified as the target set. Set2 is not needed for deletion operations.
*   Set2: Specifies the target character set for translation.

### Examples

Convert input characters from uppercase to lowercase:

```shell
echo "HELLO WORLD" | tr 'A-Z' 'a-z'
hello world
```

'A-Z' and 'a-z' are sets. Sets can be custom-defined, for example: 'ABD-}', 'bB.,', 'a-de-h', 'a-c0-9'. Sets can also include escape sequences like '\n', '\t', and other ASCII characters.

Delete characters using tr:

```shell
echo "hello 123 world 456" | tr -d '0-9'
hello  world 
```

Convert tabs to spaces:

```shell
cat text | tr '\t' ' '
```

Set complement: delete all characters from the input text that are NOT in the specified set:

```shell
echo aa.,a 1 b#$bb 2 c*/cc 3 ddd 4 | tr -d -c '0-9 \n'
 1  2  3  4
```

In this example, the complement set contains digits 0-9, spaces, and the newline character \n. Therefore, these are not deleted, while all other characters are removed.

Squeeze characters using tr: replace repeated characters with a single character:

```shell
echo "thissss is      a text linnnnnnne." | tr -s ' sn'
this is a text line.
```

Using tr for simple addition:

```shell
echo 1 2 3 4 5 6 7 8 9 | xargs -n1 | echo $[ $(tr '\n' '+') 0 ]
```

Remove '^M' (carriage return) characters caused by Windows files:

```shell
cat file | tr -s "\r" "\n" > new_file
# OR
cat file | tr -d "\r" > new_file
```

**Character classes available in tr:**

```shell
[:alnum:]: Letters and digits
[:alpha:]: Letters
[:cntrl:]: Control (non-printing) characters
[:digit:]: Digits
[:graph:]: Graphic characters
[:lower:]: Lowercase letters
[:print:]: Printable characters
[:punct:]: Punctuation marks
[:space:]: Whitespace characters
[:upper:]: Uppercase letters
[:xdigit:]: Hexadecimal digits
```

Usage:

```shell
tr '[:lower:]' '[:upper:]'
```
