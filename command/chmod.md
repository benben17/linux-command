chmod
===

Used to change the permissions of files or directories

## Synopsis

```shell
chmod [OPTION]... MODE[,MODE]... FILE...
chmod [OPTION]... OCTAL-MODE FILE...
chmod [OPTION]... --reference=RFILE FILE...
```

## Main Purpose

- Change the permissions of target files or directories using symbolic combinations.
- Change the permissions of target files or directories using octal numbers.
- Change the permissions of target files or directories based on a reference file's permissions.

## Arguments

mode: Octal mode or symbolic combination.

file: One or more files to change permissions for.

## Options

```shell
-c, --changes: Like verbose but report only when a change is made.
--no-preserve-root: Do not treat '/' specially (the default).
--preserve-root: Fail to operate recursively on '/'.
-f, --silent, --quiet: Suppress most error messages.
-v, --verbose: Output a diagnostic for every file processed.
--reference=RFILE: Use RFILE's mode instead of MODE values.
-R, --recursive: Change files and directories recursively.
--help: Display help information and exit.
--version: Display version information and exit.
```

## Return Value

Returns success unless invalid options or arguments are provided.

## Examples

> Referring to the `DESCRIPTION` section of `man chmod`:
> - `u` represents the current user (owner).
> - `g` represents users in the same group as the owner.
> - `o` represents other users.
> - `a` represents all users.
> - `r` represents read permission (octal 4).
> - `w` represents write permission (octal 2).
> - `x` represents execute permission (octal 1).
> - `X` represents execute permission only if the file is a directory or already has execute permission for some user.
> - `s` represents set user or group ID on execution (SUID/SGID).
> - `t` represents the restricted deletion flag or sticky bit.
> - `+` adds specified permissions.
> - `-` removes specified permissions.
> - `=` sets specified permissions and removes others.

```shell
Explanation of Linux file permissions:

# View current directory (including hidden files) in long format.
ls -la
  -rw-r--r--   1 user  staff   651 Oct 12 12:53 .gitmodules

# The 1st character: 'd' for directory, '-' for regular file.
# For more details, see 'info coreutils 'ls invocation'' section for '-l' option.
# Characters 2-4: Owner permissions.
# Characters 5-7: Group permissions.
# Characters 8-10: Other users' permissions.
```

```shell
# Add write permission for the group.
chmod g+w ./test.log
# Remove all permissions for other users.
chmod o= ./test.log
# Remove write permission for all users.
chmod a-w ./test.log
# Owner has all permissions, group has read/write, others have read only.
chmod u=rwx,g=rw,o=r ./test.log
# Equivalent octal representation:
chmod 764 ./test.log
# Set directory and its contents to read/write for all users.
# Note: When using '-R', ensure the current user retains execute and read permissions!
chmod -R a=rw ./testdir/
# Set file permissions based on another file.
chmod --reference=./1.log ./test.log
```

### Note

1. This command is part of the `GNU coreutils` package. For related help, see `man chmod` or `info coreutils 'chmod invocation'`.

2. Permissions of symbolic links cannot be changed; changes applied to a symbolic link affect the target file.

3. When using the `-R` option, ensure the current user retains execute and read permissions, otherwise an error will occur!
