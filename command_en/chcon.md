chcon
===

Change the SELinux security context of a file.

## Description

The **chcon command** is used to modify the security context of an object (file), such as the user, role, type, or security level. It changes the security environment of each file to the specified environment. When using the `--reference` option, the security environment of the specified file is set to be the same as that of the reference file. The `chcon` command is located at `/usr/bin/chcon`.

### Syntax

```shell
chcon [options]... CONTEXT FILE...
chcon [options]... [-u USER] [-r ROLE] [-l RANGE] [-t TYPE] FILE...
chcon [options]... --reference=RFILE FILE...
```

### Options

```shell
-h, --no-dereference: Affect symbolic links instead of the files they reference.
--reference=RFILE: Use the security environment of the specified reference file instead of a specified value.
-R, --recursive: Recursively process all files and subdirectories.
-v, --verbose: Display diagnostic information for all processed files.
-u, --user=USER: Set the target security environment for the specified user.
-r, --role=ROLE: Set the target security environment for the specified role.
-t, --type=TYPE: Set the target security environment for the specified type.
-l, --range=RANGE: Set the target security environment for the specified range.
```

The following options are used when the `-R` option is specified to set how to traverse the directory structure. If more than one option is specified, only the last one will take effect.

```shell
-H: If a command-line argument is a symbolic link to a directory, traverse the symbolic link.
-L: Traverse every symbolic link to a directory encountered.
-P: Do not traverse any symbolic links (default).
--help: Display this help message and exit.
--version: Display version information and exit.
```

### Examples

If you want to share this FTP directory with anonymous users, you need to enable the following:

```shell
chcon -R -t public_content_t /var/ftp
```

If you want the FTP directory you set up to allow file uploads, you need to set the SELinux type:

```shell
chcon -t public_content_rw_t /var/ftp/incoming
```

Allow users to access their home directory via HTTP (this setting is limited to the user's home directory homepage):

```shell
setsebool -P httpd_enable_homedirs 1
chcon -R -t httpd_sys_content_t ~user/public_html
```

If you wish to share a Samba directory with other users, you need to set:

```shell
chcon -t samba_share_t /directory
```

When sharing an rsync directory:

```shell
chcon -t public_content_t /directories
```
