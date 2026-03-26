pssh
===

Parallel SSH for batch management

## Description

The **pssh command** is a tool written in Python for executing commands on multiple servers simultaneously. It also supports copying files and is considered an excellent tool in its class, similar to `pdsh` but often seen as simpler. It requires SSH key authentication to be configured on each server.

### Installing pssh

On CentOS systems, you can install it via yum or from source:

 **Using yum** 

```shell
yum install pssh
```

 **Installing from source** 

```shell
wget http://parallel-ssh.googlecode.com/files/pssh-2.3.1.tar.gz
tar xf pssh-2.3.1.tar.gz
cd pssh-2.3.1/
python setup.py install
```

### Options

```shell
--version: View version.
--help: View help/this information.
-h: Hosts file list, format "[user@]host[:port]".
-H: Host string, format "[user@]host[:port]".
-l: User name for login.
-p: Number of concurrent threads [optional].
-o: Output directory [optional].
-e: Error output file [optional].
-t: TIMEOUT setting, 0 for unlimited [optional].
-O: SSH options.
-v: Verbose mode.
-A: Manual password input mode.
-x: Extra command-line arguments, handling white spaces, quotes, and backslashes.
-X: Extra command-line arguments, single argument mode, same as -x.
-i: Output internal processing information for each server.
-P: Print information returned by the server.
```

### Examples

Get uptime for each server:

```shell
# pssh -h ip.txt -i uptime
[1] 11:15:03 [SUCCESS] Mar.mars.he
11:15:11 up 4 days, 16:25,  1 user,  load average: 0.00, 0.00, 0.00
[2] 11:15:03 [SUCCESS] Jan.mars.he
11:15:12 up 3 days, 23:26,  0 users,  load average: 0.00, 0.00, 0.00
[3] 11:15:03 [SUCCESS] Feb.mars.he
11:15:12 up 4 days, 16:26,  2 users,  load average: 0.08, 0.02, 0.01
```

Check MySQL replication IO/SQL thread status on each server:

```shell
# pssh -h IP.txt -i "/usr/local/mysql/bin/mysql -e 'show slave status \G'"|grep Running:
             Slave_IO_Running: yes
            Slave_SQL_Running: Yes
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
```

Save results from each server:

```shell
# pssh -h IP.txt -i -o /tmp/pssh/ uptime
[1] 11:19:47 [SUCCESS] Feb.mars.he
11:19:55 up 4 days, 16:31,  2 users,  load average: 0.02, 0.03, 0.00
[2] 11:19:47 [SUCCESS] Jan.mars.he
11:19:56 up 3 days, 23:30,  0 users,  load average: 0.01, 0.00, 0.00
[3] 11:19:47 [SUCCESS] Mar.mars.he
11:19:56 up 4 days, 16:30,  1 user,  load average: 0.00, 0.00, 0.00
```

Let's look at the files and contents in /tmp/pssh/

```shell
# ll /tmp/pssh/
Total 12
-rw-r--r--. 1 root root 70 Dec  1 11:19 Feb.mars.he
-rw-r--r--. 1 root root 70 Dec  1 11:19 Jan.mars.he
-rw-r--r--. 1 root root 69 Dec  1 11:19 Mar.mars.he

# cat /tmp/pssh/*
11:19:55 up 4 days, 16:31,  2 users,  load average: 0.02, 0.03, 0.00
11:19:56 up 3 days, 23:30,  0 users,  load average: 0.01, 0.00, 0.00
11:19:56 up 4 days, 16:30,  1 user,  load average: 0.00, 0.00, 0.00
```

The above covers only a small part of the pssh command. You can adapt it to your specific scenarios for maximum effectiveness.
