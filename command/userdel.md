userdel
===

Used to delete a given user and files related to the user.

## Description

The **userdel command** is used to delete a given user and files related to the user. If no options are added, only the user account is deleted, and related files are not removed.

### Syntax

```shell
userdel (option) (parameter)
```

### Options

```shell
-f: Force the removal of the user, even if the user is currently logged in;
-r: Remove all files related to the user while deleting the user.
```

### Parameters

Username: The username to be deleted.

### Examples

The userdel command is simple. For example, if we have a user `linuxde` whose home directory is located in the `/var` directory, let's delete this user:

```shell
userdel linuxde       # Delete user linuxde, but do not delete their home directory and files;
userdel -r linuxde    # Delete user linuxde, and delete their home directory and files together;
```

Please do not use the `-r` option lightly; it will delete all the user's files and directories. Remember to back up if there are important files in the user directory before deleting.

Actually, there is a simplest way, but it is somewhat unsafe, which is to directly delete the record of the user you want to delete in `/etc/passwd`. However, it is best not to do this as `/etc/passwd` is an extremely important file, and you might make a mistake.
