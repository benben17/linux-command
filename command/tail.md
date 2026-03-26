tail
===

Output the last part of files

## Description

The **tail command** is used to output the last part of a file.
- By default, it displays the last 10 lines of the specified file.
- When multiple files are specified, it prepends each with its file name.
- If no file is specified or if the file is `-`, it reads from standard input.
- If the `NUM` value for bytes or lines is prefixed with a `+`, output starts at the `NUM`-th item from the beginning of the file, rather than the last `NUM` items.
- Suffixes for `NUM`:
  - `b`  : 512
  - `kB` : 1000
  - `k ` : 1024
  - `MB` : 1000 * 1000
  - `M ` : 1024 * 1024
  - `GB` : 1000 * 1000 * 1000
  - `G ` : 1024 * 1024 * 1024
  - `T`, `P`, `E`, `Z`, `Y` etc. follow the same logic.

### Syntax

```shell
tail (options) (parameters)
```

### Options

```shell
-c, --bytes=NUM                 Output the last NUM bytes.
-f, --follow[={name|descriptor}] Output appended data as the file grows. "name" tracks by filename.
-F                              Same as "--follow=name --retry".
-n, --lines=NUM                 Output the last NUM lines.
--pid=PID                       Used with "-f"; terminate after process PID dies.
-q, --quiet, --silent           Never output headers giving file names.
--retry                         Keep trying to open a file if it is inaccessible. Use with "--follow=name".
-s, --sleep-interval=N          With "-f", sleep for N seconds between iterations.
-v, --verbose                   Always output headers giving file names.
--help                          Display help information.
--version                       Display version information.
```

### Parameters

File list: List of files to display the end of.

### Examples

```shell
tail file # (Display the last 10 lines of file)
tail -n +20 file # (Display file from line 20 to the end)
tail -c 10 file # (Display the last 10 bytes of file)

tail -25 mail.log # Display the last 25 lines of mail.log
tail -f mail.log # Equivalent to --follow=descriptor; tracking stops if the file is renamed or deleted.
tail -F mail.log # Equivalent to --follow=name --retry; tracking continues even if the file is deleted or renamed if a new file with the same name is created.
```
