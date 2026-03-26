grpconv
===

Convert group passwords to shadow group passwords.

## Supplemental Information

The **grpconv command** is used to enable shadow group passwords. In Linux, user and group passwords are traditionally stored in `/etc/passwd` and `/etc/group`. Since these files must be readable by all users for the system to function, they present a security risk. Shadow passwords move the encrypted passwords to `/etc/shadow` and `/etc/gshadow`, which are only readable by the system administrator, while replacing the original password fields with an "x" character. This functionality can be enabled or disabled at any time; simply execute `grpconv` to enable shadow group passwords.

### Syntax

```shell
grpconv
```

### Examples

Set a group password for `cdy`:

```shell
groupmod --password 123456 cdy
cat /etc/group | grep cdy
cdy:123456:1000:     # The password '123456' is visible
```

Enable shadow passwords:

```shell
grpconv
cat /etc/group | grep cdy
cdy:x:1000:      # The password field is replaced by 'x'

cat /etc/gshadow | grep cdy
cdy:123456::      # The password has moved to the shadow file
```

Note: `/etc/gshadow` and `/etc/shadow` can only be viewed with root privileges.
