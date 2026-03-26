pstree
===

Display the derivation relationship between processes in a tree diagram.

## Description

The **pstree command** displays the derivation relationship between processes in a tree diagram, providing a clear and intuitive view of the process hierarchy.

### Syntax 

```shell
pstree(options)
```

### Options 

```shell
-a: Display the full command line for each process, including paths, parameters, or resident service markers.
-c: Disable compact notation for identical process subtrees.
-G: Use VT100 terminal line-drawing characters.
-h: Highlight the current process when listing the tree.
-H<PID>: Similar to "-h", but highlights the specified process.
-l: Use long format for displaying the tree.
-n: Sort processes by PID instead of by name.
-p: Display process IDs (PIDs).
-u: Display user names.
-U: Use UTF-8 line-drawing characters.
-V: Display version information.
```

### Examples 

Display PIDs for all current processes:

```shell
pstree -p
```

Display detailed information for all processes, using compact notation for identical process names:

```shell
pstree -a
```

Retrieve the PID of an SSH session:

```shell
pstree -p | grep ssh

#  |-sshd(1221)-+-sshd(2768)---bash(2770)-+-grep(2810)
#  |            `-sshd(2807)---sshd(2808)
```

From the output above, you can see the tree diagram of the `sshd` process and its branches. The main `sshd` process is `sshd(1221)`, with two branches `sshd(2768)` and `sshd(2807)`.
