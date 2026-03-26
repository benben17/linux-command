test
===

Evaluate conditional expressions.

## Synopsis

```shell
test [expr]
```

## Main Purpose

- Evaluate conditional expressions.

## Parameters

### File Operators:

```shell
-a FILE    True if file exists.
-b FILE    True if file is block special.
-c FILE    True if file is character special.
-d FILE    True if file is a directory.
-e FILE    True if file exists.
-f FILE    True if file exists and is a regular file.
-g FILE    True if file is set-group-id.
-h FILE    True if file is a symbolic link.
-L FILE    True if file is a symbolic link.
-k FILE    True if file has its sticky bit set.
-p FILE    True if file is a named pipe.
-r FILE    True if you can read the file.
-s FILE    True if file exists and is not empty.
-S FILE    True if file is a socket.
-t FD      True if FD is opened on a terminal.
-u FILE    True if file is set-user-id.
-w FILE    True if file is writable.
-x FILE    True if you can execute the file.
-O FILE    True if file is effectively owned by you.
-G FILE    True if file is effectively owned by your group.
-N FILE    True if file has been modified since it was last read.
    
FILE1 -nt FILE2    True if file1 is newer than file2 (according to modification date).
FILE1 -ot FILE2    True if file1 is older than file2 (according to modification date).
FILE1 -ef FILE2    True if file1 is a hard link to file2.
```    
### String Operators:

```shell
-z STRING              True if string is empty.
-n STRING              True if string is not empty.
STRING                 True if string is not empty.
STRING1 = STRING2      True if the strings are equal.
STRING1 != STRING2     True if the strings are not equal.
STRING1 < STRING2      True if STRING1 sorts before STRING2 lexicographically.
STRING1 > STRING2      True if STRING1 sorts after STRING2 lexicographically.
```

### Other Operators:

```shell
-o OPTION         True if shell option OPTION is enabled.
-v VAR            True if shell variable VAR is set.
-R VAR            True if shell variable VAR is set and is a name reference.
! EXPR            True if expr is false.
EXPR1 -a EXPR2    True if both expr1 and expr2 are true.
EXPR1 -o EXPR2    True if either expr1 or expr2 is true.
arg1 OP arg2      Arithmetic expression test; OP is one of -eq, -ne, -lt, -le, -gt, -ge; returns true if the arithmetic expression is true.
```

## Return Value

Returns 0 if the expression evaluates to success, and returns 1 if the expression evaluates to failure or if invalid parameters are given.

## Examples

```shell
# Execute a conditional expression and show the return value.
[root@pc root]$ test ! "abc" == 123; echo $?
0

# Equivalent form, note: space after the opening bracket [ and before the closing bracket ].
[root@pc root]$ [ ! "abc" == 123 ]; echo $?
0

[root@pc root]$ [[ ! "abc" == 123 ]]; echo $?
0
```


### Notes

1. This command is equivalent to `[`.
2. To write bash conditional expressions, you can use the built-in command `test`, `[`, or the compound command `[[`.
  > - For conditional expressions, see [here](http://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html#Bash-Conditional-Expressions).
  > - For an index of built-in commands, see [here](http://www.gnu.org/software/bash/manual/html_node/Builtin-Index.html#Builtin-Index).
  > - For an index of compound commands, see [here](http://www.gnu.org/software/bash/manual/html_node/Reserved-Word-Index.html#Reserved-Word-Index).
3. This command is a bash built-in; see the `help` command for related help information.
