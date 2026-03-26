pwck
===

Verify the integrity of system authentication file content and format.

## Description

The **pwck command** is used to verify the integrity of the content and format of the system authentication files `/etc/passwd` and `/etc/shadow`.

### Syntax

```shell
pwck(options)(parameters)
```

### Options

```shell
-q: Report errors only;
-s: Sort `/etc/passwd` and `/etc/shadow` by user ID;
-r: Run the command in read-only mode;
-R: Check the password files in the specified chroot environment.
```

### Parameters

*   Password file: Specifies the path to the password file.
*   Shadow file: Specifies the path to the shadow file.

### Example

```shell
pwck
user 'ftp': directory '/var/ftp' does not exist
pwck: no changes
```
After executing the `pwck` command, warnings may be displayed, such as the home directory `/var/ftp` for user `ftp` not existing. To resolve this, you have several options:
1. If you are certain these users will not be used, consider using the `userdel` command to delete them.
2. If these users are needed, you should create the corresponding directory. For example:

```shell
# Create the directory
sudo mkdir /var/ftp
# Assign ownership of the directory to the corresponding user
sudo chown ftp:ftp /var/ftp
```
3. If the packages corresponding to these users are not installed, consider installing them. Package managers (like `yum` or `apt`) typically create the necessary users and directories automatically.
