passwd
===

Change user password.

## Description

The **passwd command** is used to change a user's authentication tokens (password). It can also be used to manage password expiration, locking accounts, and more. While regular users can only change their own passwords, the system administrator (root) can change the password for any account.

### Syntax

```shell
passwd [options] [user]
```

### Options

```shell
-d, --delete    # Delete a user's password (makes the account passwordless). Root only.
-f, --force     # Force the operation.
-k, --keep-tokens # Only update expired passwords.
-l, --lock      # Lock the specified account's password.
-s, --status    # Display account status information. Root only.
-u, --unlock    # Unlock the specified account's password.
-S, --status    # Report password status for the given account.
--stdin         # Read the new password from standard input (useful for scripts).
```

### Parameters

**User**: The name of the user whose password is to be changed.

### Extended Knowledge

Files related to users and groups:

**User information:**
- `/etc/passwd`: Basic user attributes.
- `/etc/shadow`: Encrypted passwords and aging information.

**Group information:**
- `/etc/group`: Basic group attributes.
- `/etc/gshadow`: Secure group information.

**Analysis of `/etc/passwd` fields (separated by `:`):**
Example: `jack:x:503:504::/home/jack:/bin/bash`
- `jack`: Username.
- `x`: Password placeholder (actual encrypted password is in `/etc/shadow`).
- `503`: User ID (UID). 0 is root; normal users usually start from 500 or 1000 depending on the distribution.
- `504`: Group ID (GID).
- `::`: GECOS field (description/full name).
- `/home/jack`: User's home directory.
- `/bin/bash`: User's default shell.

**Analysis of `/etc/shadow` fields:**
Example: `jack:$6$...:18000:0:99999:7:::`
- `jack`: Username.
- `$6$...`: Hashed password.
- `18000`: Days since Jan 1, 1970 that the password was last changed.
- `0`: Minimum password age (days before user can change it again).
- `99999`: Maximum password age (days before user must change it).
- `7`: Warning period (days before expiration to start notifying the user).
- (Other fields include inactivity period and expiration date).

### Examples

**Changing a user's password (as root):**
```shell
[root@localhost ~]# passwd linuxde
Changing password for user linuxde.
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```

**Non-interactive password change using `--stdin`:**
```shell
[root@localhost ~]# echo "123456" | passwd --stdin linuxde
Changing password for user linuxde.
passwd: all authentication tokens updated successfully.
```

**Regular user changing their own password:**
```shell
[linuxde@localhost ~]$ passwd
Changing password for user linuxde.
(current) UNIX password: 
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```

**Locking an account:**
```shell
[root@localhost ~]# passwd -l linuxde
Locking password for user linuxde.
passwd: Success
```

**Deleting/Clearing a password:**
```shell
[root@localhost ~]# passwd -d linuxde
Removing password for user linuxde.
passwd: Success

[root@localhost ~]# passwd -S linuxde
linuxde NP 2023-10-27 0 99999 7 -1 (Empty password.)
```
Note: A passwordless account may allow login without a password depending on the system configuration.
