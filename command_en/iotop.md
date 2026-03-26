iotop
===

An interactive I/O monitor.

## Description

The `iotop` command is a `top`-like utility for monitoring disk I/O usage. It has a UI similar to `top`, showing PID, user, I/O rates, and process names. While tools like `iostat` provide per-device statistics, `iotop` allows you to identify which specific processes are responsible for I/O activity.

`iotop` is written in Python and requires Python 2.5+ and Linux kernel 2.6.20+.

### Installation

**Ubuntu:**
```shell
sudo apt-get install iotop
```

**CentOS:**
```shell
sudo yum install iotop
```

**From Source:**
```shell
wget http://guichaz.free.fr/iotop/files/iotop-0.4.4.tar.gz    
tar zxf iotop-0.4.4.tar.gz    
python setup.py build    
sudo python setup.py install
```

### Syntax

```shell
iotop [options]
```

### Options

```shell
-o : Show only processes or threads actually doing I/O.
-b : Batch mode (non-interactive), useful for logging to a file.
-n NUM : Number of iterations to run before exiting.
-d SEC : Interval between iterations in seconds.
-p PID : Monitor specific process ID.
-u USER : Monitor specific user.
```

**Interactive Shortcuts:**
- `Left/Right Arrows`: Change sorting column.
- `r`: Reverse sort order.
- `o`: Toggle "only show processes doing I/O".
- `p`: Toggle between processes and threads.
- `a`: Toggle accumulation of I/O.
- `q`: Quit.

### Examples

```shell
sudo iotop
```

Output Example:
```shell
Total DISK read:       0.00 B/s | Total DISK write:       0.00 B/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    command
    1 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init [3]
...
```
