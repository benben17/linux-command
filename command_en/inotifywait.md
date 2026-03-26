inotifywait
===

Wait for changes to files using inotify.

## Description

**Inotify** is a powerful, fine-grained, asynchronous file system monitoring mechanism. It meets various file monitoring needs, such as tracking access, read/write operations, permission changes, deletions, creations, and moves.

**inotify-tools** is a C library and a set of command-line utilities that provide a simple interface to inotify. Installing `inotify-tools` provides two commands:

- `inotifywait`: Collects information about file access. It is often not included by default in Linux distributions and requires the kernel to have inotify support enabled (which most modern distributions do).
- `inotifywatch`: Collects statistical data about the monitored file system, including the frequency of each inotify event.

Check if your kernel supports inotify:
- Check kernel version with `uname -r` (must be 2.6.13 or higher).
- Check for `/proc/sys/fs/inotify/` entries:
  ```shell
  ls /proc/sys/fs/inotify
  max_queued_events  max_user_instances  max_user_watches
  ```

### Installing inotify-tools

- Project URL: https://github.com/rvoicilas/inotify-tools

For CentOS:
```shell
tar zxvf inotify-tools-3.14.tar.gz
cd inotify-tools-3.14
./configure
make
sudo make install
```

### inotify Parameters

These parameters limit the kernel memory consumed by inotify:

- `max_queued_events`: The maximum number of events that can be queued in an inotify instance.
- `max_user_instances`: The maximum number of inotify instances per real user ID.
- `max_user_watches`: The maximum number of directories an instance can monitor.

To increase these values:
```shell
echo 104857600 > /proc/sys/fs/inotify/max_user_watches
```

### inotifywait Usage

Example script (`watchdir.sh`):
```shell
#!/bin/bash
path=$1
/usr/local/bin/inotifywait -mrq --timefmt '%d/%m/%y/%H:%M' --format '%T %w %f' -e modify,delete,create,attrib $path
```

Execution output:
```shell
./watchdir.sh /data/wsdata/tools/
04/01/13/16:34 /data/wsdata/tools/ .j.jsp.swp
...
```

### inotifywait Options

- `-m`: Monitor changes continuously.
- `-r`: Monitor directories recursively.
- `-q`: Quiet mode; print only relevant information.
- `-e`: Specify a list of events to monitor.
- `--timefmt`: Specify the time output format.
- `--format`: Specify the detailed output format for file changes.

### Monitorable Events

| Event | Description |
| --- | --- |
| access | File was read. |
| modify | File content was modified. |
| attrib | File metadata (permissions, timestamps, etc.) was modified. |
| move | File was moved. |
| create | A new file was created. |
| open | File was opened. |
| close | File was closed. |
| delete | File was deleted. |
