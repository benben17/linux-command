htpasswd
===

Create and update password files for Apache basic authentication.

## Description

The `htpasswd` command is a built-in utility for the Apache Web server. It is used to create and update files used to store usernames and passwords for basic authentication of HTTP users.

### Syntax

```shell
htpasswd [options] [passwordfile] [username]
```

### Options

```shell
-c : Create a new encrypted file.
-n : Display the encrypted username and password on the screen instead of updating the file.
-m : Use MD5 encryption for passwords (default).
-d : Use CRYPT encryption for passwords.
-p : Do not encrypt passwords (plaintext).
-s : Use SHA encryption for passwords.
-b : Enter the username and password on the command line instead of being prompted.
-D : Delete a specified user.
```

### Parameters

*   Username: The name of the user to create or update.
*   Password: The new password for the user.

### Examples

**Add a user using htpasswd**

```shell
htpasswd -bc .passwd www.example.com mypassword
```

This creates a file named `.passwd` in the current directory with the username `www.example.com` and password `mypassword`, using MD5 encryption by default.

**Add another user to an existing password file**

```shell
htpasswd -b .passwd Jack 123456
```

Remove the `-c` option to append a second user to the existing file.

**Display encrypted username and password without updating the file**

```shell
htpasswd -nb Jack 123456
```

This outputs the username and the encrypted password to the screen instead of writing to `.passwd`.

**Delete a username and password**

```shell
htpasswd -D .passwd Jack
```

**Change a password**

```shell
htpasswd -D .passwd Jack
htpasswd -b .passwd Jack newpassword
```

First, delete the user, then add them back with the new password.
