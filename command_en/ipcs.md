ipcs
===

Report System V interprocess communication facilities status.

## Description

The `ipcs` command provides information on System V interprocess communication facilities, including message queues, shared memory segments, and semaphore sets.

### Syntax

```shell
ipcs [options]
```

### Options

#### Resource Options
```shell
-a, --all         Show all facilities (default).
-q, --queues      Show active message queues.
-m, --shmems      Show active shared memory segments.
-s, --semaphores  Show active semaphore sets.
```

#### Output Options
```shell
-t, --time        Show last operation times.
-p, --pid         Show PIDs of creator and last operator.
-c, --creator     Show creator and owner IDs.
-l, --limits      Show resource limits.
-u, --summary     Show status summary.
--human           Print sizes in human-readable format.
-b, --bytes       Print sizes in bytes (affects -l only).
```

#### General Options
```shell
-i, --id <id>     Show details for a specific resource ID.
-h, --help        Display help and exit.
-V, --version     Display version information and exit.
```

### Examples

```shell
ipcs -a
------ Shared Memory Segments --------
key        shmid      owner      perms      bytes      nattch     status
0x7401833d 2654208    root      600        4          0
...
```

### Related Commands
- `ipcrm`: Remove IPC resources.
- `ipcmk`: Create IPC resources.
