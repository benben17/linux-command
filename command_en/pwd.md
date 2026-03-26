pwd
===

Display the absolute path of the current working directory.

## Description

The **pwd command** (print working directory) is used to display the current working directory of the user as an absolute path.

## Builtin Command

#### Synopsis

```shell
pwd [-LP]
```

#### Options

```shell
-L (default) Print the value of the environment variable "$PWD", which may contain symbolic links.
-P Print the physical location of the current working directory.
```

#### Return Value

Returns success unless an invalid option is provided or the current directory cannot be read.

#### Note

1. This command is a bash builtin; use the `help` command for related help information.


## External Command

#### Synopsis

```shell
pwd [OPTION]...
```

#### Main Usage

- Display the current working directory.


#### Options

```shell
-L, --logical Print the value of the environment variable "$PWD", which may contain symbolic links.
-P, --physical (default) Print the physical location of the current working directory.
--help Display help information and exit.
--version Display version information and exit.
```

#### Return Value

Returns success unless an invalid option is provided or the current directory cannot be read.

#### Note

1. This command is part of the `GNU coreutils` package; use `man pwd` or `info coreutils 'pwd invocation'` for help.
2. To enable or disable builtin commands, use the `enable` command. For priority issues with same-named commands, see the `builtin` command examples.
3. If the builtin is not disabled and no `pwd` function is defined, `pwd` refers to the bash builtin, while `/usr/bin/pwd` refers to the `coreutils` version.


## Example

View the current path:

```shell
[root@localhost var]# pwd
/var
```

Display the final target path of a symbolic link:

```shell
[root@localhost ~]# cd /var/   # Enter /var directory; there is a "mail" symbolic link here
[root@localhost var]# ls -al
total 164
...
lrwxrwxrwx  1 root root   10 Oct 17  2015 mail -> spool/mail

[root@localhost var]# cd mail/   # Enter the mail directory; mail is a symbolic link.
[root@localhost mail]# pwd       # By default, shows the logical path.
/var/mail
```

Use the `-P` parameter to display the physical path instead of the logical one:

```shell
[root@localhost mail]# pwd -P    
/var/spool/mail
```
