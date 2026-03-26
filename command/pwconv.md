pwconv
===

Enable shadow passwords for users.

## Description

The **pwconv command** is used to enable shadow passwords for users. In Linux, user and group passwords are stored in files named `passwd` and `group` in the `/etc` directory. Since these files must be readable by everyone for system operations, this presents a security risk. Shadow passwords move the encrypted passwords to the `shadow` and `gshadow` files in the `/etc` directory, which are readable only by the system administrator. The original password fields are replaced with "x", effectively strengthening system security.

### Syntax

```shell
pwconv
```

### Example

```shell
cat /etc/passwd | grep test
test:x:3001:3001::/home/test:/bin/sh
```

At this point, you can see the password field is `x`.

```shell
cat /etc/shadow | grep test
test:$6$nYOEWamm$bz07nlv/.RgJufb3FAqJJeULfwybzgxmrWqbk7O4vI0KsT6N.ujrh6dDIUcAJdfjksyuyAFDPIngZeD3cgcf.0:15022:0:99999:7:::
```
