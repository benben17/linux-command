setsebool
===

Modify the boolean values of rules within the SELinux policy.

## Description

The **setsebool command** is used to modify the boolean values of various rules within the SELinux policy. The `setsebool` and `getsebool` commands form a set of tools for modifying and querying SELinux boolean values. Commands related to SELinux policy and rule management include: `seinfo`, `sesearch`, `getsebool`, `setsebool`, and `semanage`.

### Syntax

```shell
setsebool [-P] boolean=[0|1]
```

### Options

```shell
-P: Write the setting directly to the configuration file, making the change persistent across reboots.
```

### Examples

Allow vsftpd anonymous users write permissions:

```shell
setsebool -P allow_ftpd_anon_write=1
```

If you want your FTP users to be able to access their own home directories, you need to enable:

```shell
setsebool -P ftp_home_dir 1
```

If you want to run vsftpd as a daemon, you need to enable:

```shell
setsebool -P ftpd_is_daemon 1
```

You can stop SELinux from protecting the vsftpd daemon:

```shell
setsebool -P ftpd_disable_trans 1 
```

Enable HTTP to allow CGI settings:

```shell
setsebool -P httpd_enable_cgi 1
```

Allow HTTP access to user home directories (limited to the user's home page):

```shell
setsebool -P httpd_enable_homedirs 1
chcon -R -t httpd_sys_content_t ~user/public_html
```

Allow httpd to communicate with the terminal:

```shell
setsebool -P httpd_tty_comm 1
```

Disable SELinux protection for the httpd daemon:

```shell
setsebool -P httpd_disable_trans 1
service httpd restart
```

Update SELinux settings regarding named master zones:

```shell
setsebool -P named_write_master_zones 1
```

Disable daemon protection for named:

```shell
setsebool -P named_disable_trans 1
service named restart
```

Set local NFS shares to read-only in SELinux:

```shell
setsebool -P nfs_export_all_ro 1
```

Set local NFS shares to read-write in SELinux:

```shell
setsebool -P nfs_export_all_rw 1
```

If you want to mount a remote NFS home directory locally, you need to enable:

```shell
setsebool -P use_nfs_home_dirs 1
```

If the Samba server shares directories across multiple domains:

```shell
setsebool -P allow_smbd_anon_write=1
```

To share home directories via Samba:

```shell
setsebool -P samba_enable_home_dirs 1
```

If you need to use a remote Samba server's home directory locally:

```shell
setsebool -P use_samba_home_dirs 1
```

Disable SELinux protection for the Samba daemon:

```shell
setsebool -P smbd_disable_trans 1
service smb restart
```

Allow other users to write via rsync:

```shell
setsebool -P allow_rsync_anon_write=1
```

Stop process protection for rsync:

```shell
setsebool -P rsync_disable_trans 1
```

Allow the system to use Kerberos:

```shell
setsebool -P allow_kerberos 1
```

When the system operates in a NIS environment:

```shell
setsebool -P allow_ypbind 1
```
