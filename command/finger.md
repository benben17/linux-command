finger
===

Find and display user information.

## Description

The **finger command** is used to find and display user information. It can be used for users on both local and remote hosts, and account names are case-insensitive. When executed without arguments, `finger` displays login information for all users currently on the local host, including account name, real name, login terminal, idle time, login time, and office location/phone number if available.

### Syntax

```shell
finger (options) (parameters)
```

### Options

```shell
-l: List the user's account name, real name, home directory, login shell, login time, mail status, and the contents of the .plan and .project files.
-m: Exclude searching by the user's real name.
-s: List the user's account name, real name, login terminal, idle time, login time, and office location/phone number.
-p: List the user's account name, real name, home directory, login shell, login time, and mail status, but omit the contents of the .plan and .project files.
```

If no options are specified and a username is provided, the default output style is `-l`. Otherwise, it defaults to `-s`. Note that in either format, some fields may be missing if the information is unavailable. If no parameters are specified, `finger` prints an entry for each user currently logged in.

### Parameters

Username: Specifies the user whose information is to be queried.

### Examples

Using `finger` on the local machine:

```shell
[root@localhost root]# finger
Login    Name       Tty      Idle  Login Time   Office     Office Phone
root     root       tty1        2  Dec 18 13:00
root     root       pts/0       1  Dec 18 13:05
root     root      *pts/1          Dec 18 13:10
```

To query user information on a remote machine, use the format `username@hostname`. Note that the remote host must be running a finger daemon (fingerd) to support this.
