ps
===

Report the current system's process status.

## Description

The **ps command** is used to report the current status of processes in the system. It can be paired with the `kill` command to interrupt or delete unnecessary processes at any time. The `ps` command is both fundamental and powerful, used to determine which processes are running, their status, whether they have finished, if they are zombie processes, which processes are consuming excessive resources, and more. Most process-related information can be obtained by executing this command.

### Syntax

```shell
ps (options)
```

### Options

```shell
-a: Display processes executed by all terminals, except session leaders.
a: Display all processes on the current terminal, including those of other users.
-A: Display all processes.
-c: Display CLS and PRI columns.
c: Show the actual command name of each process without paths, options, or resident service markers.
-C<command>: Specify the command name and list the status of processes for that command.
-d: Display all processes except session leaders.
-e: Same as the "A" option.
e: Display environment variables used by each process.
-f: Display UID, PPID, C, and STIME columns.
f: Display a tree structure using ASCII characters to show relationships between processes.
-g<group>: Same as the "-G" option, but can also specify by session leader name.
g: Display all processes on the current terminal, including group leaders.
-G<GID>: List the status of processes belonging to the group ID or group name.
h: Do not display the header line.
-H: Display a tree structure showing relationships between processes.
-j or j: Display process status using job control format.
-l or l: Display process status using a detailed format.
L: List column information.
-m or m: Display all threads.
n: Represent USER and WCHAN columns numerically.
-N: Display all processes except those on the terminal where the ps command is executed.
-p<PID>: Specify the process ID and list its status.
p<PID>: Same as the "-p" option, with minor differences in list format.
r: List only processes currently running on the terminal.
-s<session>: Specify the session ID and list processes belonging to that session.
s: Display process status using signal format.
S: Include data from interrupted subprocesses when listing.
-t<TTY>: Specify the terminal ID and list processes belonging to it.
t<TTY>: Same as the "-t" option, with minor differences in list format.
-T: Display all processes on the current terminal.
-u<UID>: Same as the "-U" option.
u: Display process status using a user-oriented format.
-U<UID>: List processes belonging to the user ID or user name.
U<user>: List processes belonging to the specified user.
v: Display process status using virtual memory format.
-V or V: Display version information.
-w or w: Use wide format to display process status.
x: Display all processes, not limited by terminal.
X: Display process status using old Linux i386 login format.
-y: When used with "-l", do not display the F (flag) column and replace the ADDR column with the RSS column.
-<PID>: Same as the "p" option.
--cols<width>: Set the maximum characters per line.
--columns<width>: Same as "--cols".
--cumulative: Same as the "S" option.
--deselect: Same as the "-N" option.
--forest: Same as the "f" option.
--headers: Repeat the header line.
--help: Online help.
--info: Display debugging information.
--lines<rows>: Set the number of rows for the display.
--no-headers: Same as the "h" option, with minor differences in list format.
--group<group>: Same as the "-G" option.
--Group<GID>: Same as the "-G" option.
--pid<PID>: Same as the "-p" option.
--rows<rows>: Same as "--lines".
--sid<session>: Same as the "-s" option.
--tty<TTY>: Same as the "-t" option.
--user<user>: Same as the "-U" option.
--User<UID>: Same as the "-U" option.
--version: Same as the "-V" option.
--width<width>: Same as "--cols".
```

Because `ps` supports many system types, the number of options is extensive!

### Examples

```shell
ps axo pid,comm,pcpu # View PID, name, and CPU usage of processes
ps aux | sort -rnk 4 # Sort processes by memory usage
ps aux | sort -nk 3  # Sort processes by CPU usage
ps -A # Display all process information
ps -u root # Display information for a specific user
ps -efL # View thread count
ps -e -o "%C : %p : %z : %a" | sort -k5 -nr # View processes and sort by memory usage
ps -ef # Display all process information, including the command line
ps -ef | grep ssh # Common combination of ps and grep to find a specific process
ps -C nginx # Search for a process by name or command
ps aux --sort=-pcpu,+pmem # Sort by CPU (descending) or memory (ascending)
ps -f --forest -C nginx # Display process hierarchy in tree style
ps -o pid,uname,comm -C nginx # Display child processes of a parent process
ps -e -o pid,uname=USERNAME,pcpu=CPU_USAGE,pmem,comm # Redefine labels
ps -e -o pid,comm,etime # Display process execution time
ps -aux | grep named # View detailed information of the named process
ps -o command -p 91730 | sed -n 2p # Get service name by process ID
```

List PID and related information for your current login:

```shell
ps -l
#  UID   PID  PPID        F CPU PRI NI       SZ    RSS WCHAN     S             ADDR TTY           TIME CMD
#  501   566   559     4006   0  31  0  4317620    228 -      Ss                  0 ttys001    0:00.05 /App...cOS/iTerm2 --server /usr/bin/login -fpl kenny /Ap...s/MacOS/iTerm2 --launch_shel
#  501   592   577     4006   0  31  0  4297048     52 -      S                   0 ttys001    0:00.63 -zsh
```

- F: Flag for the process; 4 indicates the user is a superuser.
- S: Status (STAT) of the process.
- UID: Owner of the process.
- PID: Process ID.
- PPID: Parent process ID.
- C: Percentage of CPU resources used.
- PRI: Priority of the process.
- NI: Nice value.
- ADDR: Kernel function pointing to the memory part of the process. "-" for running processes.
- SZ: Amount of memory used.
- WCHAN: Indicates if the process is running; "-" means running.
- TTY: Terminal associated with the user.
- TIME: CPU time consumed.
- CMD: Command executed.

> By default, `ps` only lists PIDs associated with the current `bash shell`. Thus, `ps -l` typically shows only a few PIDs.

List all processes currently in memory:

```shell
ps aux

# USER               PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
# kenny             6155  21.3  1.7  7969944 284912   ??  S    二03下午 199:14.14 /Appl...OS/WeChat
# kenny              559  20.4  0.8  4963740 138176   ??  S    二03下午  33:28.27 /Appl...S/iTerm2
# _windowserver      187  18.0  0.6  7005748  95884   ??  Ss   二03下午 288:44.97 /Syst...Light.WindowServer -daemon
# kenny             1408  10.7  2.1  5838592 347348   ??  S    二03下午 138:51.63 /Appl...nts/MacOS/Google Chrome
# kenny              327   5.8  0.5  5771984  79452   ??  S    二03下午   2:51.58 /Syst...pp/Contents/MacOS/Finder
```

- USER: The user account the process belongs to.
- PID: The process ID.
- %CPU: CPU resource usage percentage.
- %MEM: Physical memory usage percentage.
- VSZ: Amount of virtual memory used (Kbytes).
- RSS: Amount of fixed memory occupied (Kbytes).
- TTY: Terminal associated with the process. "?" if none. tty1-tty6 are local logins; pts/0 etc. are network logins.
- STAT: Current status of the process:
- R: Running or runnable.
- S: Sleeping (idle), but wakeable by signals.
- T: Traced or stopped.
- Z: Zombie process (terminated but parent has not reaped it).
- START: Time the process was started.
- TIME: Total CPU time used by the process.
- COMMAND: The actual command of the process.

List processes in a tree-like structure:

```shell
ps -axjf

# USER               PID  PPID  PGID   SESS JOBC STAT   TT       TIME COMMAND            UID   C STIME   TTY
# root                 1     0     1      0    0 Ss     ??   10:51.90 /sbin/launchd        0   0 二03下午 ??
# root                50     1    50      0    0 Ss     ??    0:10.07 /usr/sbin/syslog     0   0 二03下午 ??
# root                51     1    51      0    0 Ss     ??    0:29.90 /usr/libexec/Use     0   0 二03下午 ??
```

Find PIDs related to cron and syslog services:

```shell
ps aux | egrep '(cron|syslog)'

# root                50   0.0  0.0  4305532   1284   ??  Ss   二03下午   0:10.08 /usr/sbin/syslogd
# kenny            90167   0.0  0.0  4258468    184 s007  R+    9:23下午   0:00.00 egrep (cron|syslog)
```

Display all processes and output to a file:

```shell
ps -aux > ps001.txt
```
