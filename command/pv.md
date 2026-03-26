pv
===

Monitor the progress of data through a pipe; Pipe Viewer.

## Description

The **pv command** stands for Pipe Viewer, developed by Andrew Wood. It is used to monitor the progress of data processing through a pipeline. It provides information such as elapsed time, percentage completion (via a progress bar), current throughput rate, total data transferred, and estimated time remaining.

## Installation

```shell
# For Debian-based systems like Ubuntu
sudo apt-get install pv

# For RedHat-based systems
yum install pv
```

### Syntax

```shell
pv(options)(parameters)
pv [OPTION] [FILE]...
```

### Options

```shell
-p, --progress           Show progress bar
-t, --timer              Show elapsed time
-e, --eta                Show estimated time of arrival (completion)
-I, --fineta             Show absolute estimated time of arrival
                         (completion)
-r, --rate               Show data transfer rate counter
-a, --average-rate       Show average data transfer rate counter
-b, --bytes              Show number of bytes transferred
-T, --buffer-percent     Show percentage of transfer buffer in use
-A, --last-written NUM   Show number of bytes last written
-F, --format FORMAT      Set output format to FORMAT
-n, --numeric            Output percentage
-q, --quiet              Do not output any information

-W, --wait               Do not display anything until the first byte is transferred
-D, --delay-start SEC    Do not display anything until SEC seconds have passed
-s, --size SIZE          Set estimated data size to SIZE bytes
-l, --line-mode          Count lines instead of bytes 
-0, --null               Lines are null-terminated
-i, --interval SEC       Update every SEC seconds
-w, --width WIDTH        Assume terminal width is WIDTH characters 
-H, --height HEIGHT      Assume terminal height is HEIGHT rows
-N, --name NAME          Prefix visual information with NAME
-f, --force              Force output of standard error to terminal
-c, --cursor             Use cursor positioning escape sequences

-L, --rate-limit RATE    Limit transfer to RATE bytes per second
-B, --buffer-size BYTES  Use a buffer size of BYTES
-C, --no-splice          Never use splice(), always use read/write
-E, --skip-errors        Skip read errors in input
-S, --stop-at-size       Stop after transferring --size bytes
-R, --remote PID         Update settings of process PID

-P, --pidfile FILE       Save process ID in FILE 

-d, --watchfd PID[:FD]   Watch process PID and its open file descriptor FD

-h, --help               Display help
-V, --version            Display version information
```


### Examples

A common scenario is copying a large file from a USB drive to your computer. If you use `cp`, you won't know the status until it's finished or fails.

```shell
# Copying a file with progress display
linux [master●] % pv ~/Downloads/CentOS-7-x86_64-Minimal-1511.iso > ~/Desktop/CentOS-7-x86_64-Minimal-1511.iso
# Output information
552MiB 0:00:02 [ 212MiB/s] [==================>           ] 91% ETA 0:00:00

# -L allows you to limit the transfer rate.
# Use the -L option to limit the transfer rate to 2MB/s.
pv -L 2m /media/himanshu/1AC2-A8E3/fNf.mkv > ./Desktop/fnf.mkv 
```

Display a progress bar when copying a file (if no options are specified, -p, -t, -e, -r, and -b are used by default).

```bash
$ pv getiot.db > getiot.db.bak
```
Compress `/var/log/syslog` into a zip file while displaying progress.

```bash
$ pv /var/log/syslog | zip > syslog.zip
```

Display a progress bar when extracting with `tar`.

```bash
$ pv rootfs.tar.bz2 | tar -jxf - -C rootfs/
12.3MiB 0:00:02 [6.15MiB/s] [=========>                                     ] 21% ETA 0:00:07
````

Extraction completed.

```bash
$ pv rootfs.tar.bz2 | tar -jxf - -C rootfs/
57.8MiB 0:00:10 [5.53MiB/s] [==============================================>] 100%
```

Display characters one by one at a steady rate in the terminal.

```shell
echo "Tecmint[dot]com is a community of Linux Nerds and Geeks" | pv -qL 10
```

Compress a file and show progress.

```shell
pv /media/himanshu/1AC2-A8E3/fnf.mkv | gzip > ./Desktop/fnf.log.gz 
```

Write an ISO to disk using `dd` and use `pv` to show a progress bar.

```shell
sudo pv -cN source < /Users/kacperwang/Downloads/CentOS-7-x86_64-Everything-1511.iso | sudo dd of=/dev/disk2 bs=4m
## Progress display:
source:  5.2GiB 5:11:41 [ 503KiB/s] [=====================>       ] 71% ETA 2:01:56
```

On Linux, if executing a command or script that takes a long time, you can use `pv` to monitor the PID. Once the task is completed, you can be notified via network tools like WeChat or DingTalk.

```shell
$ pv -d $(ps -ef | grep -v grep | grep "<keyword of script or command>" | awk '{print $2}') && <execute notification script or command here>
```

### Notes

1. The option "-d, --watchfd PID[:FD]" was introduced in version 1.6.6. If you want to use it, ensure `pv` is upgraded to at least version 1.6.6.
2. The latest version of `pv` in the CentOS 7 Yum repository is 1.4.6. Version 1.6.6 is available for CentOS 8. You can download the RPM for your architecture from [here](http://www.rpmfind.net/linux/rpm2html/search.php?query=pv&submit=Search+...&system=EPEL&arch=). To install 1.6.6: `rpm -ivh pv-1.6.6-7.el8.x86_64.rpm -U`
