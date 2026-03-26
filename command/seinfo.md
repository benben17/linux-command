seinfo
===

Query how many rules are provided by the SELinux policy.

## Description

The **seinfo command** is used to query how many related rules are provided by the SELinux policy. Whether a subject process can read a target file resource depends on the SELinux policy and the rules within it. The rules define how to handle the security contexts of various target files, especially the "type" part. Related commands for managing SELinux policies and rules include `seinfo`, `sesearch`, `getsebool`, `setsebool`, and `semanage`.

### Syntax

```shell
seinfo(options)
```

### Options

```shell
-A: Lists all information, including SELinux status, rule Booleans, identities, roles, types, etc.
-t: Lists all SELinux types.
-r: Lists all SELinux roles.
-u: Lists all SELinux identities (users).
-b: Lists all rule types (Booleans).
```

### Examples

List rules related to `httpd`:

```shell
seinfo -b | grep httpd
```
