trap
===

Trap signals and other events and execute commands.

## Synopsis

```shell
trap [-lp] [[arg] signal_spec ...]
```

## Main Purpose

- Used to specify actions to be taken upon receiving signals.
- Execute cleanup tasks when a script is interrupted.

## Options

```shell
-l    Print a list of signal names and their corresponding numbers.
-p    Display the trap commands associated with each signal.
```

## Parameters

arg: The command to be executed when a signal is received.

signal_spec: The signal name or the signal number.

## Return Value

Returns 0 if the expression executes successfully. Returns 1 if `signal_spec` does not specify a valid value.

## About Signals

Signals are a mechanism for inter-process communication that provides an asynchronous software interrupt, allowing applications to receive commands (signals) sent by other programs or terminals. When an application receives a signal, there are three ways to handle it: ignore, default, or catch. After receiving a signal, a process checks its handling mechanism. If it is `SIG_IGN`, the signal is ignored; if it is `SIG_DFL`, the system's default action is taken (usually terminating the process or ignoring the signal); if a handling function (trap) is specified for the signal, the current task is interrupted to execute the handling function, and then the interrupted task resumes.

In some cases, you may not want your shell script to be interrupted during execution. For example, if a shell script is set as a user's default shell to restrict them to a specific task (like database backup), you wouldn't want the user to enter the shell state using Ctrl+C. This is where signal handling comes in.

Here are some common signals you might encounter:

| Signal Name | Signal Number | Description |
| :--- | :--- | :--- |
| SIGHUP | 1 | Issued when a user terminal connection ends (normally or abnormally). Usually, it notifies jobs within the same session that they are no longer associated with the controlling terminal. When logging into Linux, a session is assigned to the user. All programs run in this terminal belong to this session. When a user logs out, foreground and background processes with terminal output receive SIGHUP. The default action is to terminate the process. For daemons detached from the terminal, this signal is used to trigger a configuration reload. |
| SIGINT | 2 | Interrupt signal, issued when the user presses Ctrl+C. |
| SIGQUIT | 3 | Similar to SIGINT, but controlled by the QUIT character (usually Ctrl+\\). Processes exiting due to SIGQUIT produce a core file, similar to a program error. |
| SIGFPE | 8 | Issued during fatal arithmetic errors, including floating-point errors, overflows, and division by zero. |
| SIGKILL | 9 | Used to immediately terminate a program. This signal cannot be blocked, handled, or ignored. |
| SIGALRM | 14 | Timer signal, measuring real or clock time. Used by the `alarm` function. |
| SIGTERM | 15 | Termination signal. Unlike SIGKILL, it can be blocked and handled. Usually used to request a program to exit gracefully; the `kill` command generates this by default. |

## Examples

When the shell receives `HUP INT PIPE QUIT TERM`, the currently executing program will execute `exit 1`.

```shell
[root@pc root]$ trap "exit 1" HUP INT PIPE QUIT TERM
```

### 1. Cleaning Up Temporary Files

The following shows how to delete files and then exit if someone tries to interrupt the program from the terminal:

```shell
trap "rm -f $WORKDIR/work1 $WORKDIR/dataout; exit" 2
```

If the program receives signal 2, `work1` and `dataout` will be automatically deleted.

Adding signal 1 (`SIGHUP`):

```shell
$ trap "rm $WORKDIR/work1 $WORKDIR/dataout; exit" 1 2
```

### 2. Ignoring Signals

If the command listed in the trap is empty, the specified signals will be ignored upon receipt:

```shell
$ trap '' 2
```

Ignoring multiple signals:

```shell
$ trap '' 1 2 3 15
```

### 3. Resetting Traps

If you change the action taken after receiving a signal, you can omit the first parameter to reset it to the default behavior.

```shell
$ trap 1 2
```

### Notes

1. `trap -l` is equivalent to executing `kill -l`.
2. To send signals, see the `kill` command.
3. This command is a bash built-in; see the `help` command for related help information.
4. It is recommended to read the following resources to learn more:
- [GNU Official Manual: trap command](https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins.html#index-trap)
- [Linux Shell Signal trap Details](https://blog.csdn.net/elbort/article/details/8525599)
- [Bash Scripting: mktemp and trap Tutorial](http://www.ruanyifeng.com/blog/2019/12/mktemp.html)
- [Bash Built-in: trap](https://blog.csdn.net/iEearth/article/details/52612557)
