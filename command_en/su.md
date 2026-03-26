su
===

Used to switch the current user identity to another user identity

## Description

The **su command** (short for "substitute user" or "switch user") is used to switch the current user identity to another user identity. When switching, the password of the target user account must be entered.

### Syntax

```shell
su (options) (parameters)
```

### Options

```shell
-c <command>, --command=<command>: Execute the specified command and then return to the original identity.
-f, --fast: Applicable to csh and tcsh; prevents the shell from reading startup files.
-l, --login: When changing identity, also change the working directory, as well as HOME, SHELL, USER, and logname. Additionally, the PATH variable will be updated.
-m, -p, --preserve-environment: Do not change environment variables when changing identity.
-s <shell>, --shell=<shell>: Specify the shell to be executed.
--help: Display help.
--version: Display version information.
```

### Parameters

User: Specify the target user account to switch to.

### Examples

Switch to root, execute the `ls` command, and then return to the original user:

```shell
su -c ls root
```

Switch to root and pass the `-f` option to the new shell:

```shell
su root -f
```

Switch to test and change the working directory to test's home directory:

```shell
su - test
```
