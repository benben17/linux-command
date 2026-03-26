kill
===

Send a signal to processes.

## Table of Contents

- [Bash Built-in Command](#bash-built-in-command)
- [GNU Coreutils Command](#gnu-coreutils-command)

## Bash Built-in Command

### Synopsis

```shell
kill [-s sigspec | -n signum | -sigspec] pid | jobspec ...
kill -l [sigspec]
```

### Main Purpose

- Send signals to jobs or processes (can be multiple).
- List signals.

### Options

```shell
-s sig    Signal name.
-n sig    Signal number corresponding to the signal name.
-l        List signal names. If a number is provided after this option, it is assumed to be the signal number corresponding to a signal name.
-L        Equivalent to the -l option.
```

### Parameters

pid: Process ID

jobspec: Job identifier

### Return Value

Returns success unless an invalid option is given or an execution error occurs.

### Examples

```shell
[user2@pc] kill -l 9
KILL

# List all signal names:
[user2@pc] kill -l
 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL
 5) SIGTRAP      6) SIGABRT      7) SIGBUS       8) SIGFPE
 9) SIGKILL     10) SIGUSR1     11) SIGSEGV     12) SIGUSR2
13) SIGPIPE     14) SIGALRM     15) SIGTERM     16) SIGSTKFLT
17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU
25) SIGXFSZ     26) SIGVTALRM   27) SIGPROF     28) SIGWINCH
29) SIGIO       30) SIGPWR      31) SIGSYS      34) SIGRTMIN
35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3  38) SIGRTMIN+4
39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12
47) SIGRTMIN+13 48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14
51) SIGRTMAX-13 52) SIGRTMAX-12 53) SIGRTMAX-11 54) SIGRTMAX-10
55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7  58) SIGRTMAX-6
59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX

# Common signals are listed below.
# Only signal 9 (SIGKILL) can unconditionally terminate a process; other signals can be ignored by the process.

HUP     1    Hangup
INT     2    Interrupt (same as Ctrl + C)
QUIT    3    Quit (same as Ctrl + \)
KILL    9    Kill (force terminate)
TERM   15    Terminate
CONT   18    Continue (opposite of STOP, used by fg/bg commands)
STOP   19    Stop (same as Ctrl + Z)
```

```shell
# The following forms of sending the KILL signal are equivalent. There are more equivalent forms, not all listed here.
[user2@pc] kill -s SIGKILL PID
[user2@pc] kill -s KILL PID
[user2@pc] kill -n 9 PID
[user2@pc] kill -9 PID

[user2@pc] sleep 90 &
[1] 178420

# Terminate the job with job identifier 1.
[user2@pc] kill -9 %1

[user2@pc] jobs -l
[1]+ 178420 KILLED                  ssh 192.168.1.4

[user2@pc] sleep 90 &
[1] 181357

# Send STOP signal.
[user2@pc] kill -s STOP 181357

[user2@pc] jobs -l
[1]+ 181537 Stopped (signal)        sleep 90

# Send CONTINUE signal.
[user2@pc] kill -s CONT 181357

[user2@pc] jobs -l
[1]+ 181537 Running                 sleep 90 &
```

### Notes

1. Bash job control commands include `bg`, `fg`, `kill`, `wait`, `disown`, `suspend`.
2. This command is a Bash built-in; for related help information, please use the `help` command.


## GNU Coreutils Command

### Synopsis

```shell
kill [-signal|-s signal|-p] [-q value] [-a] [--] pid|name...
kill -l [number] | -L
```

### Main Purpose

- Send signals to processes (can be multiple).
- List signals.

### Options

```shell
-s, --signal signal    The signal to send; can be a signal name or number.
-l, --list [number]    Print signal names or convert a given number to a signal name. Signal names can be found in (/usr/include/linux/signal.h).
-L, --table            Similar to '-l', but outputs both signal names and numbers.
-a, --all              Do not restrict the "name-to-pid" conversion to processes with the same UID as the current process.
-p, --pid              Print the PID of the target process without sending a signal.
--verbose              Print the signal and the PID receiving it.
-q, --queue value      Use sigqueue(3) instead of kill(2). The value is an integer sent with the signal.
                           If the receiving process has installed a handler for this signal with SA_SIGINFO to sigaction(2), it can obtain
                           this data via the si_sigval field of the siginfo_t structure.
--help                 Display help information and exit.
--version              Display version information and exit.
```

### Parameters

The list of processes receiving the signal can be a mix of PIDs and names.

PID: Each PID can be one of the following four cases:

Value | Description
:--:|:--:
n | If n > 0, the process with PID n receives the signal.
0 | All processes in the current process group receive the signal.
-1 | All processes with PID > 1 receive the signal.
-n | If n > 1, all processes in process group n receive the signal. To specify a process group using the "-n" form, you must first specify a signal, or the argument must be preceded by "--", otherwise it will be treated as the signal to send.

name: All processes invoked with this name will receive the signal.

### Examples

```shell
> sleep 20 &

# List the corresponding PID.
> kill -p sleep
23021
```

### Return Value

- 0 Success.
- 1 Failure.
- 64 Partial success (when multiple processes are specified).

### Notes

1. This command is part of the `GNU coreutils` package; for related help information, please use `man -s 1 kill` or `info coreutils 'kill invocation'`.
2. To enable or disable built-in commands, see the `enable` command. For issues regarding precedence between commands of the same name, see the examples in the `builtin` command.
3. Similar commands to `kill` include `xkill`, `pkill`, `killall`, etc., used for different purposes and scenarios.

## Reference Links

[Sending signals to processes](https://bash.cyberciti.biz/guide/Sending_signal_to_Processes)
