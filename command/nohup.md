nohup
===

Run a command immune to hangups, with output to a non-tty

## Description

The **nohup command** allows you to run a program in a way that ignores hangup (SIGHUP) signals, ensuring that the process continues running even after the user logs out. The output of the command is typically redirected away from the terminal.

Whether or not the output is explicitly redirected by the user, `nohup` will attempt to append output to a file named `nohup.out` in the current directory. If the current directory is not writable, it redirects output to `$HOME/nohup.out`. If neither file can be created or opened, the command will not run. If standard error is a terminal, it is redirected to the same file descriptor as standard output.

### Syntax

```shell
nohup [options] [command [args]...]
```

### Options

```shell
--help: Display help information.
--version: Display version information.
```

### Parameters

Command and Options: The program to be executed and its arguments.

### Examples

Submit a job using `nohup`. By default, all output is redirected to `nohup.out` unless an output file is specified:

```shell
nohup command > myout.file 2>&1 &
```

In the example above, output is redirected to `myout.file`.

Download a file in the background without hanging up:

```shell
nohup wget site.com/file.zip &
```

The following command generates a `nohup.out` file in the current directory containing the program's output:

```shell
nohup ping -c 10 baidu.com &
```

Simple background execution:

```shell
nohup command &
```

Redirect output to `nohup.out` in the current directory by default:

```shell
nohup python main.py &
```

Specify a custom output file (merging standard output and standard error into `main.log`):

```shell
nohup python main.py >> main.log 2>&1 &
```

Shorthand for the above (merging both outputs):

```shell
nohup python main.py &> main.log &
```

Discard all output:

```shell
nohup python main.py &> /dev/null &
```

Discard output and save the process ID (PID) to `pidfile.txt` for easier management:

```shell
nohup python main.py &> /dev/null & echo $! > pidfile.txt
```
