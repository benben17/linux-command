getcap
===

Display the capabilities of files.

## Supplemental Information

The **getcap command** is used to examine the capabilities of files. In Linux, file capabilities are a security mechanism that allows specific privileges to be assigned to an executable file without granting it full root permissions.

### Syntax

```shell
getcap [options] [filename...]
```

### Options

```shell
-v      # Display verbose information; usually used with other options.
-p      # Display the capabilities of a process.
```

### Parameters

Filename: Specifies the path(s) of the file(s) to be examined.

### Examples

Check the capabilities of an executable file:

```shell
$ getcap /usr/bin/ping
/usr/bin/ping = cap_net_raw+ep
```

Check the capabilities of all files in the current directory:

```shell
$ getcap *
/usr/bin/ping = cap_net_raw+ep
```

If a file has no capabilities set, `getcap` will not return any output.

Check the capabilities of a process (using PID as an example):

```shell
$ getcap -p 1234
```
