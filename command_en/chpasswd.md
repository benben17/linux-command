chpasswd
===

Tool for batch updating user passwords

## Description

The **chpasswd command** is a tool for batch updating user passwords. It reads a list of user/password pairs from standard input and updates the system's password files (typically `/etc/shadow`).

### Syntax

```shell
chpasswd [options]
```

### Options

```shell
-e: The input passwords are already encrypted;
-h: Display help information and exit;
-m: Use MD5 encryption instead of DES when unsupported passwords are not encrypted.
```

### Examples

First, create a file containing user-password pairs in the format `username:password`, e.g., `abc:abc123`. The file must follow this format strictly, with no empty lines. Save it as `user.txt`, then execute the `chpasswd` command:

```shell
chpasswd < user.txt
```

This is how the `chpasswd` command is used to batch modify passwords, which is a shortcut in Linux system administration.
