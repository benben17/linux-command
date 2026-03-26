ssh
===

OpenSSH SSH client (remote login program)

## Description

The **ssh command** is the client tool in the OpenSSH suite. it provides secure encrypted communications between two untrusted hosts over an insecure network.

### Syntax

```shell
ssh [option] [parameter]
```

### Options

```shell
-1: Forces ssh to try protocol version 1 only.
-2: Forces ssh to try protocol version 2 only.
-4: Forces ssh to use IPv4 addresses only.
-6: Forces ssh to use IPv6 addresses only.
-A: Enables forwarding of the authentication agent connection.
-a: Disables forwarding of the authentication agent connection.
-b: Use the specified address on the local machine as the source address of the connection.
-C: Requests compression of all data.
-F: Specifies an alternative per-user configuration file.
-f: Requests ssh to go to background just before command execution.
-g: Allows remote hosts to connect to local forwarded ports.
-i: Specifies a file from which the identity (private key) for public key authentication is read.
-l: Specifies the user to log in as on the remote machine.
-N: Do not execute a remote command.
-o: Can be used to give options in the format used in the configuration file.
-p: Port to connect to on the remote host.
-q: Quiet mode; suppresses most warning and diagnostic messages.
-X: Enables X11 forwarding.
-x: Disables X11 forwarding.
-y: Send logging information using the syslog module.
```

### Parameters

* Remote Host: Specifies the remote SSH server to connect to.
* Command: The command to execute on the remote SSH server.

### Examples

```shell
# ssh username@remote_host
ssh user1@172.24.210.101
# Specify port
ssh -p 2211 root@140.206.185.170

# SSH Suite
ssh -p 22 user@ip  # Default username is current user, default port is 22
ssh-keygen # Generate SSH public + private keys for the current user
ssh-keygen -f keyfile -i -m key_format -e -m key_format # key_format: RFC4716/SSH2(default) PKCS8 PEM
ssh-copy-id user@ip:port # Copy current user's public key to the server's ~/.ssh/authorized_keys for passwordless login
```

Connect to a remote server:

```shell
ssh username@remote_host
```

Connect to a remote server on a specific port:

```shell
ssh -p port username@remote_host
```

Connect using a specific private key:

```shell
ssh -i path/to/private_key username@remote_host
```

Execute a command on a remote server:

```shell
ssh username@remote_host "command"
```

Copy a local file to a remote server:

```shell
scp path/to/local_file username@remote_host:/path/to/remote_directory
```

Copy a remote file to the local machine:

```shell
scp username@remote_host:/path/to/remote_file path/to/local_directory
```

Local port forwarding:

```shell
ssh -L local_port:remote_host:remote_port username@remote_host
```

Remote port forwarding:

```shell
ssh -R remote_port:local_host:local_port username@remote_host
```

### The Story Behind Port 22

> Source: [Tatu Ylonen](https://linux.cn/article-8476-1.html)

Why is the port number for SSH (Secure Shell) 22? This was not a coincidence. There is a story that I (Tatu Ylonen, the designer of the SSH protocol) have never fully told before.

#### The Story of Setting SSH Port to 22

In the spring of 1995, I wrote the initial version of the SSH protocol. At that time, telnet and FTP were widely used.

I designed SSH as a replacement for both telnet (port 23) and ftp (port 21). Port 22 was vacant. I chose the number between telnet and ftp. I felt that while the port number was a small detail, it carried a certain conviction. But how was I to get that port number? I didn't own any port numbers, but I knew people who did!

Back then, getting a port number was relatively simple. The Internet wasn't as vast as it is today; it was the early days of the Internet explosion. Port allocation was handled by IANA (Internet Assigned Numbers Authority), which at the time meant Internet pioneers Jon Postel and Joyce K. Reynolds. Jon was involved in writing many major protocol standards, such as IP (RFC 791), ICMP (RFC 792), and TCP (RFC 793).

I held Jon in high regard; he had a hand in almost every major Internet RFC!

In July 1995, just before I released ssh-1.0, I sent an email to IANA:

> From ylo Mon Jul 10 11:45:48 +0300 1995  
> From: Tatu Ylonen  
> To: Internet Assigned Numbers Authority  
> Subject: Request for a port number  
> Organization: Helsinki University of Technology, Finland  
>
> Dear IANA,
>
> I have written a program for logging in from one machine to another securely over an insecure network. It provides major functionality and security improvements over current telnet and rlogin protocols. Specifically, it protects against IP, DNS, and routing spoofing. I plan to distribute the software freely on the Internet for wide usage.
>
> I would like to have a registered privileged port number for the software. A number in the range 1-255 would be preferred, so that it can be used in the WKS fields of nameservers.
>
> I have attached a draft of the protocol standard. The software has been running locally for a few months and is ready for release once the port number has been assigned. If the assignment is handled timely, I would like to have the software ready this week. I currently use port 22 in my beta tests; if I could get this port assigned, I wouldn't have to make any changes.
>
> The name of the service in the software is ssh (Secure Shell).
>
> Yours sincerely,  
> Tatu Ylonen 

(Note: The WKS record type in the DNS protocol stands for "Well-Known Service description," a DNS record type like A or MX that describes services provided by an IP. It is rarely seen today.)

The next day, I received an email from Joyce:

> Date: Mon, 10 Jul 1995 15:35:33 -0700  
> From: jkrey@ISI.EDU  
> To: ylo@cs.hut.fi  
> Subject: Re: Request for a port number  
> Cc: iana@ISI.EDU  
> Tatu,  
> We have assigned the port number 22 for ssh, and you are currently the primary contact for that service.  
> Joyce  

And that was it! SSH was officially set to port 22!!!

On July 12, 1995, at 2:21 a.m., I announced the final beta version to my testers at the Helsinki University of Technology. That same afternoon at 5:23 p.m., I announced version 1.0.0. At 5:51 p.m., I sent out an announcement for SSH (Secure Shell) to the `cypherpunks@toad.com` mailing list, as well as several newsgroups and other lists.

#### How to Change the SSH Port Number

The SSH server runs on port 22 by default. However, for several reasons, it can be run on other ports. For example, to run multiple configurations on the same host for testing purposes. In rare cases, it can even be run without root privileges on non-privileged ports (1024 and above).

The port number can be changed in the `/etc/ssh/sshd_config` configuration file by modifying `Port 22`. The SSH server `sshd` also accepts the `-p` option. The SSH client and `sftp` program also use the `-p` option.

#### Configuring SSH for Firewall Traversal

SSH is one of the few protocols typically allowed through firewalls. Outbound SSH connections are often unrestricted, particularly in smaller or more technical organizations. Inbound SSH connections are usually limited to one or a few servers.

#### Outbound SSH Connections

Configuring outbound SSH connections in a firewall is simple. If outgoing connections are restricted, simply create a rule allowing TCP port 22 for outbound traffic. If you wish to limit destinations, restrict the rule to your organization's cloud servers or jump hosts.

#### Risks of Reverse Tunnels

While allowing outbound SSH is common, it does carry risks. SSH supports tunneling. A common technique is to set up an SSH server externally to listen for connections and then forward them back into the organization to access internal servers.

This can be very convenient for developers and system administrators to access their work remotely, but it often violates security policies (e.g., PCI, HIPAA, NIST SP 800-53) as it bypasses firewall controls. It can also be exploited by hackers or foreign intelligence agencies to leave backdoors in the organization.

#### Inbound SSH Access

For inbound access, a few points should be noted:
1. Configure the firewall to forward all port 22 traffic to a specific internal IP or a DMZ host.
2. Use different ports on the firewall to access different internal servers.
3. Require a VPN (like IPsec) before allowing SSH access.

#### Restricting SSH with iptables

iptables is the built-in host firewall in the Linux kernel. If iptables is enabled on a server, use the following commands (as root) to allow incoming SSH access:

```shell
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

To persist these rules across reboots on some systems:

```shell
service iptables save
```
