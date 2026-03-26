getent
===

Retrieve entries from Name Service Switch libraries.

## Syntax

```shell
getent [options] database [key ...]
```

## Options

```shell
-h, --help     # Display help information
-i, --no-idn   # Disable IDN encoding in lookups
-s, --service  # Service to use for lookups
-V, --version  # Display version information
```

The `database` can be any of the supported databases, such as `passwd`, `group`, `hosts`, `services`, `protocols`, or `networks`.

## Examples

1. View all known accounts:

```shell
getent passwd
```

This lists all account information from the password database (e.g., `/etc/passwd`).

2. View information for a specific account:

```shell
getent passwd someuser
```

This lists information for the specified user, such as username, UID, GID, home directory, and shell.

3. View DNS records for a specific host:

```shell
getent hosts example.com
```

This lists the host database entry for `example.com`, including its IP address.

4. View service information:

```shell
getent services http
```

This lists the service port and protocol for the `http` service.

5. View a specific group:

```shell
getent group sudo
```

This lists the members of the `sudo` group.
