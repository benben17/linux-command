tee
===

Read from standard input and write to standard output and files

## Summary

```shell
tee [OPTION]... [FILE]...
```

## Description

- Use `tee` when you need to view data content on the screen while simultaneously outputting it to a file.

### Parameters

FILE (optional): One or more files to write the output to.

### Options 

```shell
-a, --append               Append to the given FILEs, do not overwrite.
-i, --ignore-interrupts    Ignore interrupt signals (Ctrl+c has no effect).
-p                         Diagnose errors writing to non-pipes.
--output-error[=MODE]      Set behavior on write error. See MODE below.
--help                     Display help and exit.
--version                  Display version information and exit.

MODE determines behavior when a write error occurs:

'warn'           Diagnose errors writing to any output.
'warn-nopipe'    Diagnose errors writing to any output except pipes.
'exit'           Exit on error writing to any output.
'exit-nopipe'    Exit on error writing to any output except pipes.

The default MODE for the -p option is 'warn-nopipe'.
If '--output-error' is not specified, the default behavior is to exit immediately on error writing to a pipe and to diagnose errors writing to non-pipe outputs.
```

## Return Value

Returns success unless invalid options or parameters are provided.

## Examples 

```shell
# Pipe process information to stdout and overwrite into files.
ps -ef | tee info_a.log info_b.log

# Pipe process information to stdout and append into files.
ps -ef | tee -a info_a.log info_b.log
```

### Notes

1. This command is part of the `GNU coreutils` package. See `man -s 1 tee` or `info coreutils 'tee invocation'`.
2. `tee` uses a caching mechanism, typically outputting every 1024 bytes. If input is received from a pipe, data is transferred to the file only when the buffer is full. If the file content is less than 1024 bytes, the buffer is flushed once the standard input is closed.
吐
