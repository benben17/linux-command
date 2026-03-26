resize
===

Sets the terminal window size.

## Description

The **resize command** sets the terminal window size. Executing the `resize` command can set the window size of a virtual terminal.

### Syntax

```shell
resize [-cu][-s <columns> <lines>]
```

### Options

```shell
-c: Use C shell commands to change the window size, even if the user environment is not C shell.
-s <columns> <lines>: Set the vertical height and horizontal width of the terminal window.
-u: Use Bourne shell commands to change the window size, even if the user environment is not Bourne shell.
```

### Examples

Using C shell:

```shell
[root@localhost ~]# resize -c
set noglob;
setenv COLUMNS '99';
setenv LINES '34';
unset noglob;
```

Using Bourne shell:

```shell
[root@localhost ~]# resize -u
COLUMNS=99;
LINES=34;
export COLUMNS LINES;
```

Set to a specific size:

```shell
[root@localhost ~]# resize -s 80 160
```
