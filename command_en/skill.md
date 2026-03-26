skill
===

Send a signal to selected processes to freeze or manipulate them.

## Description

The **skill command** is used to send signals to selected processes. While not commonly used by beginners, it is often employed during system service optimization.

### Syntax

```shell
skill [option]
```

### Options

```shell
-f: Fast mode;
-i: Interactive mode, requires confirmation for each step;
-v: Verbose mode;
-w: Warning mode;
-V: Display version number;
-t: Specify the terminal ID where the process is running;
-u: Specify the user who started the process;
-p: Specify the process ID (PID);
-c: Specify the command name that started the process.
```

### Examples

If you find a process consuming a large amount of CPU and memory but don't want to stop it completely, consider the following `top` command output:

```shell
top -c -p 16514
23:00:44  up 12 days,  2:04,  4 users,  load average: 0.47, 0.35, 0.31
1 processes: 1 sleeping, 0 running, 0 zombie, 0 stopped
CPU states:  cpu    user    nice  system    irq  softirq  iowait    idle
           total    0.0%    0.6%    8.7%   2.2%     0.0%   88.3%    0.0%
Mem:  1026912k av, 1010476k used,   16436k free,       0k shrd,   52128k buff
                    766724k actv,  143128k in_d,   14264k in_c
Swap: 2041192k av,   83160k used, 1958032k free                  799432k cached

  PID USER     PRI  NI  SIZE  RSS SHARE stat %CPU %MEM   time CPU command
16514 oracle    19   4 28796  26M 20252 D N   7.0  2.5   0:03   0 oraclePRODB2...
```

Since you've confirmed that process 16514 is using a lot of memory, you can use the `skill` command to "freeze" it instead of stopping it.

```shell
skill -STOP 16514
```

Then, check the `top` output again:

```shell
23:01:11  up 12 days,  2:05,  4 users,  load average: 1.20, 0.54, 0.38
1 processes: 0 sleeping, 0 running, 0 zombie, 1 stopped
CPU states:  cpu    user    nice  system    irq  softirq  iowait    idle
           total    2.3%    0.0%    0.3%   0.0%     0.0%    2.3%   94.8%
Mem:  1026912k av, 1008756k used,   18156k free,       0k shrd,    3976k buff
                    770024k actv,  143496k in_d,   12876k in_c
Swap: 2041192k av,   83152k used, 1958040k free                  851200k cached

  PID USER     PRI  NI  SIZE  RSS SHARE STAT %CPU %MEM   TIME CPU COMMAND
16514 oracle    19   4 28796  26M 20252 T N   0.0  2.5   0:04   0 oraclePRODB2...
```

Now, CPU idle time has increased from 0% to 94.8%. The process is effectively frozen. After some time, you might want to wake the process up:

```shell
skill -CONT 16514
```

This method is very useful if you want to temporarily freeze a process to make room for more important tasks.

This command is versatile. If you want to stop all processes of the "oracle" user, you can do it with one command:

```shell
skill -STOP oracle
```

You can use the username, PID, command, or terminal ID as arguments. The following command stops all `rman` commands:

```shell
skill -STOP rman
```

As you can see, `skill` determines the type of argument you provide (PID, user ID, or command) and acts accordingly. This can lead to issues if you have a user and a command with the same name. A classic example is the "oracle" process, usually run by the user "oracle". To be explicit, you can use a parameter to specify the type. To stop a command named "oracle":

```shell
skill -STOP -c oracle
```

The `snice` command is similar to `skill` but is used to change the priority of a process rather than stopping it. First, check `top` output:

```shell
  PID USER     PRI  NI  SIZE  RSS SHARE STAT %CPU %MEM   TIME CPU COMMAND
    3 root      15   0     0    0     0 RW    0.0  0.0   0:00   0 kapmd
13680 oracle    15   0 11336  10M  8820 T     0.0  1.0   0:00   0 oracle
13683 oracle    15   0  9972 9608  7788 T     0.0  0.9   0:00   0 oracle
13686 oracle    15   0  9860 9496  7676 T     0.0  0.9   0:00   0 oracle
13689 oracle    15   0 10004 9640  7820 T     0.0  0.9   0:00   0 oracle
13695 oracle    15   0  9984 9620  7800 T     0.0  0.9   0:00   0 oracle
13698 oracle    15   0 10064 9700  7884 T     0.0  0.9   0:00   0 oracle
13701 oracle    15   0 22204  21M 16940 T     0.0  2.1   0:00   0 oracle
```

Now, decrease the priority of the "oracle" processes by 4 points (higher value means lower priority):

```shell
snice +4 -u oracle
  PID USER     PRI  NI  SIZE  RSS SHARE STAT %CPU %MEM   TIME CPU COMMAND
16894 oracle    20   4 38904  32M 26248 D N   5.5  3.2   0:01   0 oracle
```

Notice the NI column (nice value) is now 4, and the priority (PRI) is 20 instead of 15.
