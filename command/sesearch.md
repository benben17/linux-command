sesearch
===

Query detailed rules in SELinux policy.

## Description

While the `seinfo` command can be used to query how many rules are provided by an SELinux policy, the **sesearch command** is used to query the detailed rules for a specific type or boolean value. Commands related to SELinux policy and rule management include: `seinfo`, `sesearch`, `getsebool`, `setsebool`, and `semanage`.

### Syntax

```shell
sesearch [-a] [-s source_type] [-t target_type] [-b boolean]
```

### Options

```shell
-a: List all relevant information for the type or boolean value.
-t: Followed by a type, e.g., -t httpd_t.
-b: Followed by a boolean rule, e.g., -b httpd_enable_ftp_server.
```

### Examples

Find information related to target file resource type `httpd_sys_content_t`:

```shell
sesearch -a -t httpd_sys_content_t
```

Find all information where the source process is `httpd_t` and the target file type is related to `httpd`:

```shell
sesearch -s httpd_t -t httpd_* -a
```

Check how many rules are set for the boolean `httpd_enable_homedirs`:

```shell
sesearch -b httpd_enable_homedirs -a
```
