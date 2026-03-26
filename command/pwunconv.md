pwunconv
===

Disable shadow passwords for users.

## Description

The **pwunconv command** is the opposite of `pwconv`. it is used to disable shadow passwords for users by moving the encrypted passwords from the `shadow` file back into the `passwd` file.

### Syntax

```shell
pwunconv
```

### Example

```shell
pwunconv     # Disable shadow passwords
cat /etc/passwd | grep test     # Password is now back in the passwd file
test:$6$nYOEWamm$bz07nlv/.RgJufb3FAqJJeULfwybzgxmrWqbk7O4vI0KsT6N.ujrh6dDIUcAJdfjksyuyAFDPIngZeD3cgcf.0:3001:3001::/home/test:/bin/sh

ls /etc/shadow     # Check for the shadow file; it should no longer exist
ls: cannot access /etc/shadow: No such file or directory
```
