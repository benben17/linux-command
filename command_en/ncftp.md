ncftp
===

An enhanced FTP client

## Description

The **ncftp command** is an enhanced FTP client that is significantly more powerful than traditional FTP commands. `ncftp` is a standout among text-mode FTP programs, featuring transfer rate display, download progress, automatic resume, bookmarks, and support for firewalls and proxy servers.

### Syntax

```shell
ncftp [options] [ftp_server]
```

### Options

```shell
-u: Specify the username for logging into the FTP server.
-p: Specify the password for logging into the FTP server.
-P: Specify a non-standard TCP port for the FTP server (default is 21).
-m: Attempt to create the destination directory before transferring (useful for directory transfers).
-R: Recursively transfer subdirectories.
```

### Parameters

FTP Server: Specifies the hostname or IP address of the remote FTP server.

### Installation

```shell
wget ftp://ftp.ncftp.com/ncftp/ncftp-3.2.3-src.tar.gz
tar zxvf ncftp-3.2.3-src.tar.gz
cd ncftp-3.2.3/
./configure --prefix=/usr/local/ncftp
make && make install
```

### Examples

Upload all files and directories from the local `/etc/` directory to the `flv/games/` directory on the FTP server (the directory will be created if it does not exist).

```shell
/usr/local/ncftp/bin/ncftpput -u username -p password -P 21 -m -R 192.168.162.137 flv/games/ /etc/*
```

**Usage Notes**

Basic commands in `ncftp` are similar to standard FTP. Type `help` for a list of commands. Use `help <command>` for detailed help on a specific command. Commands starting with `l` are executed locally, while others operate on the remote FTP server.

Additional local file system commands:

*   `lls`: List files in the local current directory.
*   `lmkdir`: Create a local directory.
*   `lrename`: Rename a local file.
*   `lpwd`: Display the current local path.
*   `lchmod`: Change local file permissions.
*   `lpage`: Display local file content.
*   `lrm`: Delete a local file.
*   `lrmdir`: Delete a local directory.
```
