journalctl
===

Query the systemd journal.

## Description

`journalctl` is used to retrieve logs from the systemd journal. It is available on almost all Linux distributions that use systemd (e.g., Fedora, Ubuntu, Debian, SUSE, Arch).

### Syntax

```shell
journalctl [OPTIONS...] [MATCHES...]
```

### Options

```shell
--system               # Show system logs.
--user                 # Show user logs for the current user.
-M --machine=CONTAINER # Operate on a local container.
-S --since=DATE        # Show entries not older than a specific date/time.
-U --until=DATE        # Show entries not newer than a specific date/time.
-b --boot[=ID]         # Show logs from the current or a specific boot.
--list-boots           # List recorded boot IDs.
-k --dmesg             # Show kernel messages from the current boot.
-u --unit=UNIT         # Show logs for a specific systemd unit.
-t --identifier=STR    # Show entries with a specific syslog identifier.
-p --priority=RANGE    # Show entries with specific priorities (0-7 or names).
-e --pager-end         # Jump to the end of the logs in the pager.
-f --follow            # Follow the journal (real-time output).
-n --lines[=INT]       # Number of journal entries to show.
-r --reverse           # Show the newest entries first.
-o --output=MODE       # Change output mode (short, verbose, json, json-pretty, cat, etc.).
--utc                  # Show time in UTC.
-x --catalog           # Add explanatory help texts to log messages where available.
-a --all               # Show all fields, including long or non-printable ones.
-q --quiet             # Suppress privilege warnings.
--no-pager             # Do not pipe output to a pager.
--vacuum-size=BYTES    # Reduce journal size below a specific limit.
--vacuum-time=TIME     # Remove journal files older than a specific time.
```

### Examples

**Filtering Logs:**

Show all logs since the current boot:
```shell
journalctl -b
```

Show logs from the previous boot:
```shell
journalctl -b -1
```

Show only errors and more critical messages:
```shell
journalctl -p err..alert
# Or using numbers: journalctl -p 3..1
```

Show logs since a specific time:
```shell
journalctl --since="2023-10-30 18:00:00"
journalctl --since "20 min ago"
```

Follow logs in real-time:
```shell
journalctl -f
```

Show logs for a specific service:
```shell
journalctl -u nginx.service
```

Show kernel logs:
```shell
journalctl -k
```

**Maintenance:**

Limit journal size to 100MB:
```shell
journalctl --vacuum-size=100M
```

Remove logs older than 2 weeks:
```shell
journalctl --vacuum-time=2weeks
```
