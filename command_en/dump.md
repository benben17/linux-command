dump
===

Used for backing up ext2 or ext3 file systems.

## Description

The **dump** command is used to back up ext2 or ext3 file systems. It can back up a directory or an entire file system to a specified device, or back it up into a large file.

### Syntax

```shell
dump [options] [parameters]
```

### Options

```shell
-0123456789: Backup level.
-b<block size>: Specify the block size in KB.
-B<number of blocks>: Specify the number of blocks per volume.
-c: Change the default density and capacity for backup tapes.
-d<density>: Set the tape density in BPI.
-f<device name>: Specify the backup device.
-h<level>: Files tagged with "nodump" will not be backed up when the backup level is equal to or greater than the specified level.
-n: Notify all users in the "operator" group when the backup requires administrator intervention.
-s<tape length>: Length of the backup tape in feet.
-T<date>: Specify the time and date for the backup.
-u: After the backup is completed, record the backup file system, level, date, and time in /etc/dumpdates.
-w: Similar to -W, but only displays files that need to be backed up.
-W: Display files that need to be backed up along with their last backup level, time, and date.
```

### Parameters

Backup source: Specify the file, directory, or file system to be backed up.

### Examples

Back up all contents of the `/home` directory to the `/tmp/homeback.bak` file with backup level `0` and record related information in `/etc/dumpdates`:

```shell
dump -0u -f /tmp/homeback.bak /home
```

Back up all contents of the `/home` directory to the `/tmp/homeback.bak` file with backup level `1` (only back up data that has changed since the last level `0` backup) and record related information in `/etc/dumpdates`:

```shell
dump -1u -f /tmp/homeback.bak /home
```

Through the backup levels of the `dump` command, full + incremental backup or full + differential backup can be achieved. Combined with `crontab`, unattended backups can be implemented.
