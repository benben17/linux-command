scp
===

Copy files between local and remote hosts securely.

## Description

The **scp command** is used for copying files remotely under Linux. A similar command is `cp`, but `cp` only performs copies locally and cannot work across servers. Furthermore, `scp` transmissions are encrypted, which might slightly affect the speed. When your server's hard drive becomes read-only, `scp` can help you move files out. Additionally, `scp` consumes very few resources and does not significantly increase system load, which is where `rsync` falls far short. Although `rsync` may be slightly faster than `scp`, when there are many small files, `rsync` can cause very high disk I/O, while `scp` basically does not affect normal system use.

### Syntax

```shell
scp(options)(parameters)
```

### Options

```shell
-1: Use SSH protocol version 1.
-2: Use SSH protocol version 2.
-4: Use IPv4.
-6: Use IPv6.
-B: Run in batch mode.
-C: Use compression.
-F: Specify an SSH configuration file.
-i: identity_file; reads the key file (e.g., AWS .pem) used for transmission from the specified file. This parameter is passed directly to ssh.
-l: Specify bandwidth limit.
-o: Specify SSH options.
-P: Specify the port number of the remote host.
-p: Preserves modification times, access times, and permission modes of the files.
-q: Do not display the copy progress.
-r: Copy recursively.
```

### Parameters

* Source file: Specifies the source file to be copied.
* Target file: The target file. Format is `user@host:filename`.

### Examples

The command to copy from remote to local is similar to the command above; just swap the order of the last two parameters.

**Copy a file from a remote machine to a local directory:**

```shell
scp root@10.10.10.10:/opt/soft/nginx-0.5.38.tar.gz /opt/soft/
```

This downloads the `nginx-0.5.38.tar.gz` file from the `/opt/soft/` directory on the 10.10.10.10 machine to the local `/opt/soft/` directory.

**Copy a file from AWS to a local directory:**

```shell
scp -i amazon.pem ubuntu@10.10.10.10:/usr/local/openvpn_as/etc/exe/openvpn-connect-2.1.3.110.dmg openvpn-connect-2.1.3.110.dmg
```

This downloads the OpenVPN installation file from the 10.10.10.10 machine to the current local directory.

**Copy a directory from a remote machine to local:**

```shell
scp -r root@10.10.10.10:/opt/soft/mongodb /opt/soft/
```

This downloads the `mongodb` directory from `/opt/soft/` on the 10.10.10.10 machine to the local `/opt/soft/` directory.

**Upload a local file to a specified directory on a remote machine:**

```shell
scp /opt/soft/nginx-0.5.38.tar.gz root@10.10.10.10:/opt/soft/scptest
# Specify port 2222
scp -rp -P 2222 /opt/soft/nginx-0.5.38.tar.gz root@10.10.10.10:/opt/soft/scptest
```

This copies the file `nginx-0.5.38.tar.gz` from the local `/opt/soft/` directory to the `opt/soft/scptest` directory on the remote machine 10.10.10.10.

**Upload a local directory to a specified directory on a remote machine:**

```shell
scp -r /opt/soft/mongodb root@10.10.10.10:/opt/soft/scptest
```

This uploads the local directory `/opt/soft/mongodb` to the `/opt/soft/scptest` directory on the remote machine 10.10.10.10.
