smbpasswd
===

Samba user and password management tool.

## Description

The **smbpasswd command** is part of the Samba suite and is used to add or delete Samba users and change their passwords.

### Syntax

```shell
smbpasswd [option] [parameter]
```

### Options

```shell
-a: Add a user to the smbpasswd file;
-c: Specify the Samba configuration file;
-x: Delete a user from the smbpasswd file;
-d: Disable the specified user in the smbpasswd file;
-e: Enable the specified user in the smbpasswd file;
-n: Set the specified user's password to null.
```

### Parameters

Username: Specify the user whose SMB password is to be modified.
