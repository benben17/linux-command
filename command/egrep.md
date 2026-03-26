egrep
===

Search for specified strings within files using extended regular expressions.

## Description

The **egrep** command is used to search for specified strings within files. The execution effect of `egrep` is similar to `grep -E`. Its syntax and parameters are the same as the `grep` command. The difference lies in how the pattern is interpreted: `egrep` uses extended regular expression (ERE) syntax, while `grep` uses basic regular expression (BRE) syntax. Extended regular expressions are more powerful and standardized than basic regular expressions.

### Syntax

```shell
egrep [options] [pattern] [file1, file2, ...]
```

### Examples

Display lines in files that match the criteria. For example, to find files containing the string "Linux" in the current directory:

```shell
egrep Linux *
```

Result:

```shell
# Lines containing "Linux" in testfile
testfile:hello Linux!
testfile:Linux is a free Unix-type operating system.
testfile:This is a Linux testfile!
testfile:Linux
testfile:Linux

# Lines containing "Linux" in testfile1
testfile1:helLinux!
testfile1:This a Linux testfile!

# Lines containing "Linux" in testfile_2
testfile_2:Linux is a free unix-type opterating system
testfile_2:Linux test
```

Filter out comment lines and blank lines:

```shell
egrep -v '^\s*(#|$)' filename
```
