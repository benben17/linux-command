grpunconv
===

Disable shadow group passwords.

## Supplemental Information

The **grpunconv command** is used to disable shadow group passwords. It moves the password information from the `/etc/gshadow` file back into the `/etc/group` file.

### Syntax

```shell
grpunconv
```

### Examples

Before disabling:

```shell
cat /etc/gshadow | grep cdy
cdy:123456::
```

Disable shadow passwords:

```shell
grpunconv
# After execution, /etc/gshadow might be removed or emptied depending on the system configuration.
```

Check that the password has been copied back to `/etc/group`:

```shell
cat /etc/group | grep cdy
cdy:123456:1000:
```
