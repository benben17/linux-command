screen
===

Used for switching between command-line terminals.

## Description

**Screen** is a free software developed by the GNU Project for switching between command-line terminals. Users can simultaneously connect to multiple local or remote command-line sessions and switch between them freely. GNU Screen can be thought of as a command-line interface version of a window manager. It provides a unified interface and corresponding functions for managing multiple sessions.

**Session Recovery**

As long as the Screen process itself has not terminated, any session running within it can be recovered. This is particularly useful for remote users—even if the network connection is interrupted, the user does not lose control of the opened command-line sessions. Simply log in to the host again and execute `screen -r` to recover the session. Similarly, when leaving temporarily, you can execute the `detach` command to suspend Screen (moving it to the background) while ensuring that the programs inside continue to run normally. This is very similar to VNC in a graphical interface.

**Multi-window**

In the Screen environment, all sessions run independently with their own IDs, inputs, outputs, and window buffers. Users can switch between different windows using shortcuts and freely redirect the input and output of each window. Screen implements basic text operations such as copy and paste, and provides a scrollback-like function to view the history of the window's status. Windows can also be partitioned, named, and monitored for background activity.

**Session Sharing**

Screen allows one or more users to log in to a session multiple times from different terminals and share all characteristics of the session (e.g., seeing exactly the same output). It also provides a window access mechanism that allows windows to be password-protected.

Official GNU Screen website: http://www.gnu.org/software/screen/

### Syntax

```shell
# screen -AmRvx -[ls -wipe][-d <job_name>][-h <lines>][-r <job_name>][-s ][-S <job_name>]
```

### Options

```shell
-A: Adjusts all windows to the current terminal size.
-d <job_name>: Detaches the specified screen job.
-h <lines>: Specifies the number of lines for the window buffer.
-m: Forces the creation of a new screen job, even if already inside a screen job.
-r <job_name>: Resumes a detached screen job.
-R: Attempts to resume a detached job first. If none is found, a new screen job is created.
-s: Specifies the shell to be executed when creating a new window.
-S <job_name>: Specifies the name of the screen job.
-v: Displays version information.
-x: Resumes a previously detached screen job.
-ls or --list: Displays all current screen jobs.
-wipe: Checks all current screen jobs and deletes those that are no longer usable.
```

### Common screen parameters

```shell
screen -S yourname -> Create a new session named yourname
screen -ls -> List all current sessions
screen -r yourname -> Resume the session named yourname
screen -d yourname -> Remotely detach a session
screen -d -r yourname -> End the current session and resume the session named yourname
```

In each screen session, all commands start with `Ctrl+a` (C-a).

```shell
C-a ? -> Show all key binding information
C-a c -> Create a new window running a shell and switch to it
C-a n -> Next; switch to the next window
C-a p -> Previous; switch to the previous window
C-a 0..9 -> Switch to window 0..9
Ctrl+a [Space] -> Cycle through windows 0 to 9
C-a C-a -> Switch between the two most recently used windows
C-a x -> Lock the current window; requires the user password to unlock
C-a d -> Detach; temporarily leave the current session, moving the current screen session (which may contain multiple windows) to the background. You return to the state before entering screen. Processes in the session continue to run even after logout.
C-a z -> Move the current session to the background; use the shell command 'fg' to return.
C-a w -> Show the list of all windows
C-a t -> Time; show the current time and system load
C-a k -> Kill window; forcibly close the current window
C-a [ -> Enter copy mode; in this mode, you can scroll, search, and copy like using [vi]
    C-b Backward, PageUp 
    C-f Forward, PageDown 
    H (uppercase) High; move cursor to the top-left corner
    L Low; move cursor to the bottom-left corner
    0 Move to the beginning of the line
    $ Move to the end of the line
    w Forward one word
    b Backward one word
    Space Press once to mark the start of the region, twice to mark the end
    Esc Exit copy mode
C-a ] -> Paste; paste the content selected in copy mode
```

### Using Screen

**Installing screen**

Popular Linux distributions (such as Red Hat Enterprise Linux) usually come with the screen utility. If not, it can be downloaded from the GNU Screen official website.

```shell
[root@TS-DEV ~]# yum install screen
[root@TS-DEV ~]# rpm -qa|grep screen
screen-4.0.3-4.el5
[root@TS-DEV ~]#
```

**Creating a new window**

After installation, simply typing `screen` will start it. However, a session started this way has no name. In practice, it is recommended to name each screen session for easy identification:

```shell
[root@TS-DEV ~]# screen -S david 
```

After screen starts, it creates the first window (window No. 0) and opens a default system shell (usually bash). When you type `screen`, you immediately return to the command prompt as if nothing happened, but you have entered the world of Screen. You can also add parameters after the screen command to open a specific program directly:

```shell
[root@TS-DEV ~]# screen vi david.txt
```

Screen creates a single-window session running `vi david.txt`. Exiting `vi` will exit the window/session.

**Viewing windows and window names**

After opening multiple windows, you can use the shortcut `C-a w` to list all current windows. In a text terminal, this list appears at the bottom-left; in a terminal emulator under X, it appears in the title bar. The window list usually looks like this:

```shell
0$ bash  1-$ bash  2*$ bash  
```

In this example, I have opened three windows. The `*` indicates the current window (window 2), and the `-` indicates the window I was in before the last switch (window 1).

By default, Screen names windows with a combination of the index and the running program name. You can use `C-a A` to rename the current window.

**Session Detaching and Resuming**

You can temporarily detach from a screen session without interrupting the programs running in the windows, and reconnect (attach) later. For example, open a screen window to edit `/tmp/david.txt`:

```shell
[root@TS-DEV ~]# screen vi /tmp/david.txt
```

To exit temporarily, type `C-a d`. Screen will provide a "detached" prompt.

To find the session later:

```shell
[root@TS-DEV ~]# screen -ls
```

Reconnect to the session:

```shell
[root@TS-DEV ~]# screen -r 12865
```

Everything remains as it was.

If you did not detach a Screen session on another machine, you cannot resume it directly. You can use the following command to forcibly detach the session from its current terminal and move it to the new terminal:

**Clearing dead sessions**

If a session dies for some reason (e.g., the process was manually killed), `screen -ls` will show the session as "dead". Use the `screen -wipe` command to clear it.

**Closing or Killing a Screen Session**

Normally, when you exit the last program in a window (usually the shell), that window closes. Another way to close a window is to use `Ctrl+a` then `k`, and press `y` when prompted to kill the session. This kills the current window and its running processes.

If the last window in a Screen session is closed, the entire Screen session exits, and the screen process terminates.

You can also use `C-a :` and then type the `quit` command to exit the Screen session. Note that this kills all windows and exits all running programs.

Additionally, here is another command to quickly kill a Screen session:

```shell
[root@TS-DEV ~]# screen -ls   # List existing sessions
[root@TS-DEV ~]# screen -XS "session_id_or_name" quit
```

**Example:**

```shell
[root@TS-DEV ~]# screen -ls
There are screens on:
	11235.test	(01/25/2021 03:35:31 PM)	(Detached)
1 Sockets in /run/screen/S-root.
[root@TS-DEV ~]# screen -XS 11235 quit
# or
[root@TS-DEV ~]# screen -XS test quit
```

### Advanced Screen Applications

**Session Sharing**

Session sharing is a fun way to use session recovery. Suppose you and a friend are logged into the same machine as the same user from different locations. After you create a screen session, your friend can run:

```shell
[root@TS-DEV ~]# screen -x
```

This command will attach your friend's terminal to your screen session without detaching yours. You and your friend now share the same session. If you are in the same window, it's like sitting in front of the same monitor.

**Session Locking and Unlocking**

Screen allows you to lock a session using `C-a s`. Once locked, the screen will not respond to any input (though input is still received by the processes in Screen). Use `C-a q` to unlock.

You can also use `C-a x` to lock the session with the user's password.

**Sending commands to a screen session**

You can operate a Screen session from outside using the `screen` command, which is convenient for scripting. For example:

```shell
[root@TS-DEV ~]# screen -S sandy -X screen ping www.baidu.com
```

This command creates a new window in the session named "sandy" and runs the `ping` command in it.

**Screen Splitting**

You can split the screen into different regions. Use `C-a S` for horizontal splitting. Version 4.00.03 and later also support vertical splitting with `C-a |`. Use `C-a <tab>` to switch between regions.

Use `C-a X` to close the current region, or `C-a Q` to close all regions except the current one.

**Copy/Paste Mode**

Use `C-a [` or `C-a <Esc>` to enter copy/paste mode. Move the cursor like in vi, use the spacebar to mark the start and end of a region. Use `C-a ]` to paste the content.

**More Screen Features**

GNU Screen provides rich customization via `/etc/screenrc` and `$HOME/.screenrc`. You can set options, customize key bindings, set auto-start windows, enable multi-user mode, and more.
