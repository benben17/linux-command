whoami
===

Print the user name associated with the current effective user ID

## Synopsis

```shell
whoami [OPTION]...
```

## Description

- Prints the user name associated with the current effective user ID.

## Options

```shell
--help       Display help and exit.
--version    Display version and exit.
```

## Return Value

Returns 0 on success and non-zero on failure.

## Examples

```shell
[root@localhost ~]# whoami
root
```

### Note

1. This command is equivalent to `id -un`.
2. `whoami` vs `logname`: If you log in as `root` and then `su` to `user2`, `whoami` will return `user2`, while `logname` will still return `root`.
3. This command is part of the `GNU coreutils` package. For more help, see `man -s 1 whoami`.
