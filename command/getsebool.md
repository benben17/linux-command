getsebool
===

Query the boolean values of SELinux policies.

## Supplemental Information

The **getsebool command** is used to query the boolean values of various rules within the SELinux policy. Related commands for SELinux policy and rule management include: `seinfo`, `sesearch`, `getsebool`, `setsebool`, and `semanage`.

### Syntax

```shell
getsebool [-a] [boolean_name]
```

### Options

```shell
-a: List the settings of all booleans on the current system.
```

### Examples

Query all boolean settings on the system:

```shell
getsebool -a
NetworkManager_disable_trans --> off
allow_console_login --> off
allow_cvs_read_shadow --> off
allow_daemons_dump_core --> on
....(remaining output omitted)....
```

Query if `httpd_enable_homedirs` is off, and turn it off if it is not:

```shell
getsebool httpd_enable_homedirs
setsebool -P httpd_enable_homedirs=0    # 0 is off, 1 is on
```
