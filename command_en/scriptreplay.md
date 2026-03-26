scriptreplay
===

Replay all operations of a terminal session.

## Description

**scriptreplay** is used to replay all user operations and command output from a terminal session, based on the terminal data file and timing log file recorded by the `script` command. In short, it replays everything that happened in the terminal session rather than re-running the commands. For example, character typing and deletions from when the user entered a command are also replayed. It is ideal for tutorial demonstrations. Furthermore, a terminal session recorded on machine A using `script` can be replayed on machine B using `scriptreplay`.

### Syntax

```shell
scriptreplay [options] [-t] timingfile [typescript [divisor]]
```

### Options

```shell
-t, --timing file         # The name of the file containing the timing information.
-s, --typescript file     # The name of the file containing the terminal data information.
-d, --divisor number      # Speed up the replay by dividing the timing intervals by the specified number.
                          # -d 2 means the replay speed is twice the original input speed; -d 0.1 means 10 times slower.
-m, --maxdelay number     # Specifies the maximum delay between commands (in seconds).
                          # -m 2 means if the interval between two commands is greater than 2 seconds, it will be replayed as 2 seconds.
-V, --version             # Display version information and exit.
-h, --help                # Display help text and exit.
```

### Parameters

* Timing log file: The name of the file storing timing information.
* Terminal data file: The name of the file storing terminal data information.

### Examples

```shell
# Replay terminal content; the first parameter is the timing log, the second is the terminal data.
scriptreplay time.file command.log
# Replay terminal content with a speed divisor of 1 and a maximum delay of 2 seconds between commands.
scriptreplay -d 1 -m 2 -t time.file -s command.log
```

**Record terminal content to files:**

```shell
zfb@localhost:~$ script -t 2>time.file -a -f command.log
Script started, file is command.log
zfb@localhost:~$ echo "hello, world"
hello, world
zfb@localhost:~$ echo $(date "+%Y-%m-%d %H:%M:%S")
2020-12-23 20:48:46
zfb@localhost:~$ echo "Bye"
Bye
zfb@localhost:~$ ls -al
total 20
drwxr-xr-x  2 zfb zfb 4096 Dec 23 20:48 .
drwxr-xr-x 37 zfb zfb 4096 Dec 23 20:49 ..
-rw-r--r--  1 zfb zfb    0 Dec 23 19:03 a.txt
-rw-r--r--  1 zfb zfb   12 Dec 23 19:04 b.txt
-rw-r--r--  1 zfb zfb 2744 Dec 23 20:49 command.log
-rw-r--r--  1 zfb zfb  790 Dec 23 20:49 time.file
zfb@localhost:~$ exit
Script done, file is command.log
zfb@localhost:~$
```

**Replay terminal content:**

```shell
zfb@localhost:~$ scriptreplay -d 1 -m 2 -t time.file -s command.log
zfb@localhost:~$ echo "hello, world"
hello, world
zfb@localhost:~$ echo $(date "+%Y-%m-%d %H:%M:%S")
2020-12-23 20:48:46
zfb@localhost:~$ echo "Bye"
Bye
zfb@localhost:~$ ls -al
total 20
drwxr-xr-x  2 zfb zfb 4096 Dec 23 20:48 .
drwxr-xr-x 37 zfb zfb 4096 Dec 23 20:49 ..
-rw-r--r--  1 zfb zfb    0 Dec 23 19:03 a.txt
-rw-r--r--  1 zfb zfb   12 Dec 23 19:04 b.txt
-rw-r--r--  1 zfb zfb 2744 Dec 23 20:49 command.log
-rw-r--r--  1 zfb zfb  790 Dec 23 20:49 time.file
zfb@localhost:~$ exit

zfb@localhost:~$
```

Only the command `scriptreplay -d 1 -m 2 -t time.file -s command.log` was entered by the user; everything else is automatically presented (with visual effects consistent with real user operations). The timestamp `2020-12-23 20:48:46` proves this is a replay of the record, not a re-execution of the commands. This means `time.file` and `command.log` can be moved to any machine supporting the `scriptreplay` command to dynamically reproduce the terminal session.
