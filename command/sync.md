sync
===

Flush file system buffers

## Description

The **sync command** is used to force changed blocks to disk and update the super block.

In Linux/Unix systems, file or data processing typically involves placing data into memory buffers first, then writing to disk at an appropriate time to improve system efficiency. The `sync` command can be used to force data in memory buffers to be written to disk immediately. Users usually do not need to execute the `sync` command manually, as the system automatically performs `update` or `bdflush` operations to write buffer data to disk. Manual execution is only necessary if these operations cannot run or if the user needs to perform an abnormal shutdown.

### Syntax

```shell
sync (options)
```

### Options

```shell
-d, --data             Sync only file data, not unnecessary metadata.
-f, --file-system      Sync the file systems containing the specified files.
--help: Display help.
--version: Display version information.
```

### Buffer and Cache

*   buffer: Improves efficiency for writing to disk.
*   cache: Improves efficiency for reading from disk.

To improve efficiency, Linux places data in a buffer before writing it to disk. Data is not committed to disk immediately. If the system restarts at this point, data loss may occur.

The `sync` command flushes file system buffers, ensuring data is physically written to disk and allowing buffers to be released. Therefore, it is common to run `sync` after writing important data to disk.

Even without manual execution, the Linux system periodically synchronizes data.
