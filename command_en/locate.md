locate
===

A tool for finding files by name, often faster than `find`

## Description

The **locate** command allows users to quickly search the file system for specified files. It works by querying a database that contains the names and paths of all files in the system, rather than searching the file system itself. In most distributions, the database is automatically updated periodically via a cron job.

`locate` is fast because it searches a database updated by the `updatedb` program. However, it may not find files that were created or renamed very recently. By default, `updatedb` runs daily; this schedule can be modified in `crontab`.

`locate` searches for files or directories that match the given pattern. Patterns can include wildcards (like `*` or `?`). For example, searching for `kcpa*ner` will find any file or directory starting with `kcpa` and ending with `ner`, such as `kcpartner`.

While `locate` performs a similar function to `find`, it is much faster due to the indexing. You can run `updatedb` manually to force an immediate index update.

### Syntax

```shell
locate [-d path | --database=path] [-e | -E | --[non-]existing] [-i |
       --ignore-case] [-0 | --null] [-c | --count] [-w | --wholename] [-b |
       --basename] [-l N | --limit=N] [-S | --statistics] [-r | --regex ]
       [--regextype R] [--max-database-age D] [-P | -H | --nofollow] [-L |
       --follow] [--version] [-A | --all] [-p | --print] [--help] pattern...
```

### Options

```shell
-b, --basename      # Match only the base name of the path
-c, --count         # Output only the count of matching entries
-d, --database PATH # Use the specified database instead of the default /var/lib/mlocate/mlocate.db
-e, --existing      # Only print entries for files that currently exist
-0, --null          # Separate entries with NUL in the output
-S, --statistics    # Print statistics about each database instead of searching
-q, --quiet         # Quiet mode; do not display error messages
-P, --nofollow, -H  # Do not follow trailing symbolic links when checking file existence
-l, --limit, -n N   # Limit the output (or count) to N entries
-r, --regexp REGEXP # Use a basic regular expression
    --regex         # Use an extended regular expression
-i, --ignore-case   # Ignore case distinctions
-V, --version       # Display version information
-h, --help          # Display help information
```

### Examples

Example 1: Find all files related to `pwd`:

```shell
root ~ # locate pwd
/bin/pwd
/etc/.pwd.lock
/sbin/unix_chkpwd
/usr/bin/pwdx
/usr/include/pwd.h
...
```

Example 2: Search for all files in `/etc` starting with `sh`:

```shell
root ~ # locate /etc/sh
/etc/shadow
/etc/shadow-
/etc/shells
```

Example 3: Search for all files in `/etc` starting with `m`:

```shell
root ~ # locate /etc/m
/etc/magic
/etc/magic.mime
/etc/mailcap
/etc/mailcap.order
...
```

Ignore case when searching for files in the home directory starting with `r`:

```shell
locate -i ~/r
```
