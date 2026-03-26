nologin
===

Politely refuse a user from logging into the system

## Description

The **nologin command** politely refuses a user from logging into the system and displays a message. If a login attempt is made with such an account, an entry is added to the system log and the message "This account is currently not available" is printed to the terminal. These accounts are typically used for service or system accounts that need to start processes but should not have interactive login privileges.

### Syntax

```shell
nologin
```

### Examples

**Disabling user login on Linux:**

When a user's login is disabled, they cannot access the system shell but may still be able to log into services like FTP or SAMBA. During system maintenance, you may want to disable individual or all users from logging in to ensure normal operation.

1.  **Disable a specific user (e.g., user `lynn`):**

```shell
passwd -l lynn
```

This locks the account for `lynn`, preventing them from logging in.

```shell
passwd -u lynn
```

This unlocks the `lynn` account, allowing them to log in again.

2.  **Change the user's login shell in `/etc/passwd`:**

```shell
vi /etc/passwd
```

Change the shell to `/sbin/nologin`:

```shell
lynn:x:500:500::/home/lynn:/sbin/nologin
```

The user will no longer be able to log in.

3.  **Disable all users (except root) from logging in:**

```shell
touch /etc/nologin
```

This prevents all non-root users from logging into the system.
