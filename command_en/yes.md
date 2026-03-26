yes
===

Repeatedly output a specified string.

## Supplemental Information

The **yes command** outputs a specified string repeatedly until the process is killed. If no arguments are provided, it defaults to outputting "y".

### Syntax

```shell
yes (parameters)
```

### Parameters

String: The string to be repeatedly printed.

### Examples

```shell
[root@localhost ~]# yes testline

testline
testline
testline
testline
testline
testline
testline
testline
...Repeatedly prints "testline" until interrupted by Ctrl+C.
```
