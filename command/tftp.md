tftp
===

Transfer files between the local machine and a TFTP server using the TFTP protocol

## Description

The **tftp command** is used to transfer files between the local machine and a TFTP server using the TFTP protocol.

TFTP is the simplest network protocol for downloading remote files, implemented based on the UDP protocol. An embedded Linux TFTP development environment includes two aspects: first, tftp-server support on the Linux server side, and second, tftp-client support on the embedded target system. Since u-boot itself has built-in tftp-client support, the embedded target system does not need configuration. Below is a detailed introduction to the tftp-server configuration on the Linux server side.

### Syntax

```shell
tftp [options] [parameters]
```

### Options

```shell
-c: Specify commands to be executed immediately after a successful connection to the tftp server;
-m: Specify the file transfer mode. It can be ASCII or Binary;
-v: Display detailed instruction execution process;
-V: Display instruction version information.
```

### Parameters

Host: Specifies the IP address or hostname of the TFTP server to connect to.

### Examples

**1. Install TFTP server**

Requires three software packages: xinetd, tftp, and tftp-server.

If internet access is available, install via yum:

```shell
yum install xinetd
yum install tftp
yum install tftp-server
```

If internet access is not available, install the provided RPM packages directly:

```shell
rpm -ivh xinetd-2.3.14-18.fc9.i386.rpm
rpm -ivh tftp-0.48-3.fc9.i386.rpm
rpm -ivh tftp-server-0.48-3.fc9.i386.rpm
```

**2. Configure TFTP server**

Modify the `/etc/xinetd.d/tftp` file, changing `disable=yes` to `disable=no`. The main task is to set the root directory of the TFTP server and enable the service. The modified file should look like this:

```shell
service tftp
{
       socket_type           =dgram
       protocol              =udp
       wait                  =yes
       user                  =root
       server                =/usr/sbin/in.tftpd
       server_args           =-s  /home/mike/tftpboot -c
       disable               =no
       per_source            =11
       cps                   =100 2
       flags                 =IPv4
}
```

Note: Modify `server_args= -s <path> -c`, where `<path>` is your tftp-server root directory. The `-s` parameter specifies chroot, and `-c` allows file creation.

**3. Start the TFTP server and disable the firewall**

```shell
/etc/init.d/iptables stop        # Disable firewall
sudo /sbin/service xinetd start
# OR
service xinetd restart
/etc/init.d/xinetd start
```

Seeing [OK] on startup is enough.

**4. Check if the TFTP service is enabled**

```shell
netstat -a | grep tftp
```

The result `udp 0 0 *:tftp *:*` indicates that the service is running and the TFTP configuration was successful.

**5. Using TFTP**

Copy a file to the TFTP server directory, then start the TFTP software on the host for a simple test.

```shell
tftp 192.168.1.2
tftp>get <download file> 

tftp>put <upload file>
tftp>q
```

**6. TFTP command usage is as follows**

```shell
tftp your-ip-address
```

Operations within TFTP:

*   connect: Connect to a remote TFTP server
*   mode: File transfer mode
*   put: Upload file
*   get: Download file
*   quit: Exit
*   verbose: Display detailed processing information
*   trace: Display packet path
*   status: Display current status information
*   binary: Binary transfer mode
*   ascii: ASCII transfer mode
*   rexmt: Set packet transmission timeout
*   timeout: Set retransmission timeout
*   help: Help information
*   ?: Help information

**7. If "AVC Denial, click icon to view" error persists and files cannot be transferred, make the following changes**

Modify `/etc/sysconfig/selinux`, set `SELINUX` to `disabled`, and use the command `setenforce 0` to apply the SELinux configuration.

**8. TFTP command usage in Busybox**

Format:

```shell
tftp [option] ... host [port]
```

These options are required for downloading or uploading files:

```shell
-g: Download file (get)
-p: Upload file (put)
-l: Local filename (local file)
-r: Remote filename (remote file)
```

For example, to download `embedexpert` from remote host 192.168.1.2, enter:

```shell
tftp -g -r embedexpert 192.168.1.2
```
