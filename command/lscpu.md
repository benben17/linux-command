lscpu
===

Display information about the CPU architecture

## Description

The **lscpu command** gathers CPU architecture information from `sysfs` and `/proc/cpuinfo`.

### Syntax

```shell
lscpu [OPTION]...
```

### Options

```shell
 -a, --all               # Print both online and offline CPUs (default for -e).
 -b, --online            # Print online CPUs only (default for -p).
 -c, --offline           # Print offline CPUs only.
 -e, --extended[=<list>] # Display the CPU information in an extended human-readable format.
 -p, --parse[=<list>]    # Optimize the command output for easy parsing.
 -s, --sysroot <dir>     # Use the specified directory as system root.
 -x, --hex               # Use hexadecimal masks for CPU sets.

 -h, --help     # Display help and exit.
 -V, --version  # Output version information and exit.
```

### Parameters

```shell
Available columns for -e and -p:
           CPU  Logical CPU number.
          CORE  Logical core number.
        SOCKET  Logical socket number.
          NODE  Logical NUMA node number.
          BOOK  Logical book number.
         CACHE  How caches are shared between CPUs.
  POLARIZATION  CPU dispatching mode on virtual hardware.
       ADDRESS  Physical address of a CPU.
    CONFIGURED  Whether the hypervisor has allocated the CPU.
        ONLINE  Whether Linux is currently using the CPU.
```

### Examples

```shell
[root@localhost ~]# lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    1
Core(s) per socket:    4
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 30
Model name:            Intel(R) Xeon(R) CPU           X3430  @ 2.40GHz
Stepping:              5
CPU MHz:               2394.055
BogoMIPS:              4788.11
Virtualization:        VT-x
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              8192K
NUMA node0 CPU(s):     0-3
```

Check CPU core numbers to distinguish between performance and efficiency cores (on architectures that support it):

```shell
[root@localhost ~]# lscpu -e
CPU NODE SOCKET CORE L1d:L1i:L2:L3 ONLINE MAXMHZ    MINMHZ
0   0    0      0    0:0:0:0       Yes    3600.0000 800.0000
1   0    0      1    1:1:1:0       Yes    3600.0000 800.0000
2   0    0      2    2:2:2:0       Yes    3600.0000 800.0000
3   0    0      3    3:3:3:0       Yes    3600.0000 800.0000
4   0    0      0    0:0:0:0       Yes    3600.0000 800.0000
5   0    0      1    1:1:1:0       Yes    3600.0000 800.0000
6   0    0      2    2:2:2:0       Yes    3600.0000 800.0000
7   0    0      3    3:3:3:0       Yes    3600.0000 800.0000
```
