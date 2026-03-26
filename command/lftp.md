lftp
===

An excellent file client program

## Description

The **lftp** command is an excellent file client program that supports various file transfer protocols, including FTP, SFTP, HTTP, and FTPS. lftp supports tab completion; if you forget a command, double-pressing the Tab key will show the available options.

### Syntax

```shell
lftp (options) (parameters)
```

### Options

```shell
-f: Specify a script file for lftp to execute;
-c: Execute the specified commands and then exit;
--help: Display help information;
--version: Display the version number.
```

### Parameters

Site: The IP address or domain name of the site to visit.

### Examples

**Logging into FTP**

```shell
lftp username:password@ftp_address:port (default is 21)
```

You can also log in without a username first, and then use the `login` command within the lftp interface to log in with a specific account (password will not be displayed).

**Viewing Files and Changing Directories**

```shell
ls
cd path/to/ftp/directory
```

**Downloading**

While `get` works, you can also use:

```shell
mget -c *.pdf    # Download all PDF files with resume support (continue).
mirror aaa/      # Download the entire aaa directory, including subdirectories.
pget -c -n 10 file.dat   # Download file.dat using up to 10 threads with resume support. The default thread count can be set via pget:default-n.
```

**Uploading**

Similarly, `put` and `mput` are used for files.

```shell
mirror -R local_directory_name
```

Upload the local directory recursively (including subdirectories) to the FTP site.

**Mode Settings**

```shell
set ftp:charset gbk
```

If the remote FTP site uses GBK encoding, set this accordingly. Replace `gbk` with `utf8` if needed.

```shell
set file:charset utf8
```

Set the local charset to UTF-8.

```shell
set ftp:passive-mode 1
```

Enable passive mode. Some sites require either passive or active mode to log in; this switch controls that. `0` means do not use passive mode.

**Bookmarks**

The command line also supports bookmarks. At the lftp prompt:

```shell
bookmark add ustc
```

This saves the current FTP site with the label `ustc`. Later, from the shell terminal, you can simply run `lftp ustc` to automatically log in and enter the directory.

```shell
bookmark edit
```

Invokes an editor to manually modify bookmarks. Bookmarks are stored in a simple text file where usernames and passwords might be visible.

**Configuration File**

```shell
vim /etc/lftp.conf
```

Typically, I add these lines:

```shell
set ftp:charset gbk
set file:charset utf8
set pget:default-n 5
```

This avoids having to enter these commands every time. You can use Tab and `help` within lftp to see other `set` options.
