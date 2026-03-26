hostnamectl
===

Query or change the system hostname.

## Supplemental Information

`hostnamectl` is used to query and change the system hostname and related settings.

### Syntax

```bash
hostnamectl [OPTIONS...] COMMAND ...
```

### Commands

```bash
status                 # Show current hostname settings
set-hostname NAME      # Set system hostname
set-icon-name NAME     # Set icon name for host
set-chassis NAME       # Set chassis type for host
set-deployment NAME    # Set deployment environment for host
set-location NAME      # Set location for host
```

### Options

```bash
-h, --help              # Show this help
    --version           # Show package version
    --no-ask-password   # Do not prompt for password
-H, --host=[USER@]HOST  # Operate on a remote host
-M, --machine=CONTAINER # Operate on a local container
--transient, --static, --pretty  
                        # When used with status, only print the selected hostname.
```

### Examples

Display hostname settings:

```bash
$ hostnamectl status
```

Change the hostname (permanently, without needing a reboot):

```bash
$ sudo hostnamectl set-hostname newname
```
