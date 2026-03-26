script
===

Record all operations of a terminal session.

## Description

The **script** command is used to record all user operations and command outputs in a terminal session. In short, it records everything that happens in the terminal, functioning like a terminal video recorder. For example, when a user enters a command, character typing and deletions are also recorded. All operations and terminal echoes are stored in a log file in `raw` format, known as the terminal data file. Timing information is stored separately in another log file, known as the timing log file. Use the `exit` command or the shortcut `Ctrl + D` to stop recording.

### Syntax

```shell
script(options)(parameters)
```

### Options

```shell
-a, --append              # Append the terminal session information to the file (preserves original content).
-c, --command command     # Runs the command instead of an interactive shell. This starts script, runs the command, and then exits.
                          # The command can be any command executable in a terminal session.
-e, --return              # Return the exit status of the child process.
-f, --flush               # Write content to the log file immediately whenever the terminal content changes.
--force                   # Allow the default terminal data output file to be a symbolic link.
-o, --output-limit size   # Limit the size of the terminal data file and timing log file. The child process exits when this limit is reached.
                          # Units can be: KiB(=1024), KB(=1000), MiB(1024*1024), MB(=1000*1000), etc.
                          # Also supports GiB, TiB, PiB, EiB, ZiB, YiB, GB, TB, PB, EB, ZB, YB.
-q, --quiet               # Quiet mode. Does not show start and exit prompts for the script command.
-t[file], --timing[=file] # Output timing information to standard error (stderr) or a file.
-V, --version             # Display version information and exit.
-h, --help                # Display help text and exit.
```

### Parameters

* Terminal data file: Sets the filename for storing terminal data information.

### Examples

```shell
script                             # Starts recording; by default, creates a file named 'typescript' in the current directory.
script command.log                 # Starts recording; creates a file named 'command.log' in the current directory.
script -t 2>time.file command.log  # Starts recording; creates 'command.log' for terminal data and 'time.file' for timing logs.
```

**Record terminal information in append mode:**

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

Then, the user can view the terminal data file:

```shell
zfb@localhost:~$ cat command.log
Script started on 2020-12-23 20:48:25+08:00 [TERM="xterm-256color" TTY="/dev/pts/0" COLUMNS="75" LINES="30"]
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

Script done on 2020-12-23 20:49:04+08:00 [COMMAND_EXIT_CODE="0"]
zfb@localhost:~$
```

Only the `cat command.log` command was entered by the user; everything else is automatically presented. The timestamp `2020-12-23 20:48:46` proves this is a reproduction of the record, not a re-execution of the commands. This means `time.file` and `command.log` can be moved to any machine to reproduce the command input and terminal echoes.

**Record server user session operations:**

Edit `/etc/profile` as `root` and append the following to the end of the file:

```bash
if [ $UID -ge 0 ]
then
    exec /usr/bin/script -t 2>/var/log/script-records/$USER-$UID-`date +%Y%m%d`.time -a -f -q /var/log/script-records/$USER-$UID-`date +%Y%m%d`.log
fi
```

Then create a directory as `root` to store the terminal operation information for all users on the server:

```bash
sudo mkdir -p /var/log/script-records/
sudo chmod 733 /var/log/script-records/
```

Finally, execute `source /etc/profile`. All operations performed by any user (`UID ≥ 0`) in the terminal will be recorded silently and stored on a daily basis.
