rcp
===

Make file copying between two Linux hosts simpler.

## Description

The **rcp** (remote copy) command is used to copy files between two Linux hosts. With proper configuration, copying files between hosts can be done without a password, making it as simple as a local file copy.

### Syntax

```shell
rcp [options] [parameters]
```

### Options

```shell
-p: Preserve source file or directory attributes, including owner, group, permissions, and timestamps.
-r: Recursive mode; process files and subdirectories within the specified directory.
-x: Encrypt all data transmitted between the two Linux hosts.
-D: Specify the port number of the remote server.
```

If no remote username is specified, the current username is used. If the path on the remote machine contains special shell characters, it must be enclosed in backslashes `\\`, double quotes `""`, or single quotes `''` to ensure all shell metacharacters are correctly interpreted on the remote side. Note that `rcp` does not prompt for a password; it typically uses the `rsh` command for transport.

### Parameters

Source file: Specifies the source file to be copied. Multiple source files can be provided.

### Examples

**Requirements for using rcp**

If the system uses `/etc/hosts`, ensure it contains entries for the remote host. Configuration process:

*Only for the root user:*
1. Create a `.rhosts` file in the root home directory on both systems and add the respective hostnames. Ensure IP and hostname mappings are in `/etc/hosts`.
2. Enable the `rsh` service (disabled by default on many distributions like RedHat). Use `ntsysv` or similar tools to enable it, then restart `xinetd`.
3. In `/etc/pam.d/`, comment out the line `auth required /lib/security/pam_securetty.so` in the `rsh` configuration to allow root access.

**Copy `test1` from the current directory to a remote system named `webserver1`:**

```shell
rcp test1 webserver1:/home/root/test3
```

In this case, `test1` is copied to the remote directory `/home/root/test3` with the original name `test1`. If only the hostname is provided, `rcp` copies the file to the user's remote home directory.

**Copy a file and rename it on the remote system:**

```shell
rcp test1 webserver1:/home/root/test3
```

Here, `test1` is copied to the remote directory `/home/root/` and renamed to `test3`.

**Copy a file from a remote system to the local directory:**

```shell
rcp remote_hostname:remote_file local_file
```

**Copy `test2` from remote system `webserver1` to the current directory:**

```shell
rcp webserver1:/home/root/test2 .
```

The `.` represents the current directory. `test2` is copied locally with its original name.

**Copy a file to another local directory or with a new name:**

```shell
rcp webserver1:/home/root/test2 otherdir/
rcp webserver1:/home/root/test2 otherdir/otherfile
```

**Copy a directory to a remote system:**

To copy a local directory and its contents recursively:

```shell
rcp -r local_dir remote_hostname:remote_dir
```

**Copy the `work` subdirectory to the `products` directory on `webserver1`:**

```shell
rcp -r work webserver1:/home/root/products
```

This creates a `work` directory inside `/home/root/products` on the remote host (assuming the destination path exists).

**Copy a directory from a remote system:**

To copy a remote directory and its contents to the local system:

```shell
rcp -r remote_hostname:remote_dir local_dir
```

**Copy the remote directory `work` to the current local directory:**

```shell
rcp -r webserver1:/home/root/work .
```
