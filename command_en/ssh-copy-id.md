ssh-copy-id
===

Install your public key in a remote machine's authorized_keys

## Description

The **ssh-copy-id command** copies a local public key to the `authorized_keys` file on a remote host. It also ensures that the remote user's home directory, `~/.ssh`, and `~/.ssh/authorized_keys` have the correct permissions.

**ssh-copy-id** uses SSH to log into the remote server, typically via password authentication. Therefore, `PasswordAuthentication` should be enabled in the remote server's `sshd_config`:
Set `PasswordAuthentication` to `yes` in `/etc/ssh/sshd_config`, then restart `sshd`.

### Syntax

```shell
ssh-copy-id [-i [identity_file]] [user@]machine
```

### Options

```shell
-i: Specify the identity file (public key).
```

### Examples

1. Install the local public key to the remote host:

```shell
ssh-copy-id user@server
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```
