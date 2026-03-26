ifstat
===

Report network interface statistics.

## Description

The `ifstat` command is a tool for reporting network interface activity, similar to how `iostat` or `vmstat` report other system metrics. `ifstat` is often not installed by default and may require manual installation from source.

### Download

```shell
Official Site: http://gael.roualland.free.fr/ifstat/
wget http://gael.roualland.free.fr/ifstat/ifstat-1.1.tar.gz
```

### Installation

```shell
tar -zxvf ifstat-1.1.tar.gz
cd ifstat-1.1
./configure            
make
sudo make install # Usually installs to /usr/local/bin/
```

Confirm installation: `which ifstat` should return `/usr/local/bin/ifstat`.

### Options

```shell
-l : Monitor loopback interfaces (lo). By default, ifstat monitors all non-loopback interfaces.
-a : Monitor all detectable network interfaces.
-z : Hide interfaces with no traffic.
-i : Monitor a specific interface (e.g., -i eth0).
-s : Equivalent to -d snmp:[comm@][#]host[/nn]], query a remote host via SNMP.
-h : Display short help message.
-n : Disable periodic header display.
-t : Add a timestamp to the beginning of each line.
-T : Report total bandwidth for all monitored interfaces.
-w : Use fixed column width.
-W : Wrap output if it's wider than the terminal.
-S : Keep status updates on the same line (similar to bmon).
-b : Display bandwidth in kbits/s instead of kbytes/s.
-q : Quiet mode; suppress warnings.
-v : Display version information.
-d : Specify a driver to collect statistics.
```

### Examples

Default usage:

```shell
[root@localhost ifstat-1.1] # ifstat
       eth0                eth1       
 KB/s in  KB/s out   KB/s in  KB/s out
    0.07      0.20      0.00      0.00
    0.07      0.15      0.58      0.00
```

Monitor all interfaces with totals and timestamps:

```shell
[root@localhost ifstat-1.1]# ifstat -tT
  time           eth0                eth1                eth2                eth3               Total      
HH:MM:ss   KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out
16:53:04      0.84      0.62   1256.27   1173.05      0.12      0.18      0.00      0.00   1257.22   1173.86
16:53:05      0.57      0.40      0.57      0.76      0.00      0.00      0.00      0.00      1.14      1.17
```

Monitor all detectable interfaces:

```shell
[root@localhost ifstat-1.1] # ifstat -a
        lo                 eth0                eth1       
 KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out
    0.00      0.00      0.28      0.58      0.06      0.06
    0.00      0.00      1.41      1.13      0.00      0.00
```
