tailf
===

Output the last part of a file and follow growth, typically used for log tracking

## Description

The **tailf command** is nearly identical to `tail -f`, but is more similar to `tail --follow=name`. It can continue tracking even if the file is renamed, making it ideal for monitoring the growth of log files. Unlike `tail -f`, it does not access the disk if the file is not growing. `tailf` is particularly suitable for laptops as it reduces disk access and saves power. Note that `tailf` is a compiled C binary, not a script, and may not be installed on all Linux distributions.

### Differences between tailf and tail -f

1. `tailf` reads the file incrementally from the beginning, whereas `tail -f` reads from the end.
2. `tailf` checks for file growth using the filename and the `stat` system call; `tail -f` uses the opened file descriptor. (Note: `tail` can also track by filename, but it uses `fstat` rather than `stat`. Consequently, by default, `tail` may not realize if a file is deleted, while `tailf` will).

### Syntax

```shell
tailf logfile # Dynamically track the log file, initially printing the last 10 lines.
```

### Options

```shell
-n, --lines NUMBER  # Output the last N lines.
-NUMBER             # Same as `-n NUMBER`.
-V, --version       # Output version information and exit.
-h, --help          # Display help and exit.
```

### Parameters

Target: Specify the target log file.

### Examples

```shell
tailf log/WEB.LOG 
tailf -n 5 log2014.log   # Display the last 5 lines of the file
```
