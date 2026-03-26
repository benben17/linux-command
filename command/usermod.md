usermod
===

Used to modify basic user information.

## Description

The **usermod command** is used to modify basic user information. The usermod command does not allow you to change the account name of a user who is currently logged in. When the usermod command is used to change the user ID, you must ensure that the user is not running any programs on the computer. You need to manually change the user's crontab files and at job files. Using a NIS server requires changing related NIS settings on the server.

### Syntax

```shell
usermod (option) (parameter)
```

### Options

```shell
-c<comment>: Modify the comment string for the user account;
-d<home_dir>: Modify the user's login directory. This only modifies the home directory configuration in /etc/passwd and does not automatically create a new home directory; usually used with -m;
-m<move_home>: Move the user's home directory to a new location. Cannot be used alone; generally used with -d;
-e<expire_date>: Modify the expiration date of the account;
-f<inactive>: Modify the number of days after a password expires until the account is disabled;
-g<group>: Modify the group the user belongs to;
-G<group>: Modify the supplementary groups the user belongs to;
-l<login_name>: Modify the user account name;
-L: Lock the user's password, making it invalid;
-s<shell>: Modify the shell used after the user logs in;
-u<uid>: Modify the user ID;
-U: Unlock the password.
```

### Parameters

Login name: Specifies the login name of the user whose information is to be modified.

### Examples

Add `newuser2` to the `staff` group:

```shell
usermod -G staff newuser2
```

Modify the username of `newuser` to `newuser1`:

```shell
usermod -l newuser1 newuser
```

Lock account `newuser1`:

```shell
usermod -L newuser1
```

Unlock account `newuser1`:

```shell
usermod -U newuser1
```

Add a user to a group:

```shell
apk add shadow # Install the shadow package, usermod command is included in it
usermod -aG group user # Add user to the group
```

The `-a` parameter indicates append and is only used with the `-G` parameter to add a user to supplementary groups.

Modify user home directory:

```
[root@node-1 ~]# useradd lutixiaya
[root@node-1 ~]# ls /home
lutixiaya
[root@node-1 ~]# usermod -md /data/new_home lutixiaya
[root@node-1 ~]# ls /home/
[root@node-1 ~]# ls /data/
new_home
```
