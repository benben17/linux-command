useradd
===

Create a new system user.

## Description

The **useradd command** is used to create a new system user in Linux. useradd can be used to set up user accounts. After the account is created, use `passwd` to set the account password. `userdel` can be used to delete accounts. Accounts created with the useradd command are actually stored in the `/etc/passwd` text file.

In Slackware, the adduser command is a script program that interactively obtains user account information and then passes it to the actual useradd command to create the new user, making it easier for administrators to create user accounts. In Red Hat Linux, the **adduser command** is a symbolic link to the useradd command; both are actually the same command.

### Syntax

```shell
useradd (option) (parameter)
```

### Options

```shell
-b, --base-dir BASE_DIR  # The default base directory for the system if -d HOME_DIR is not specified. If this option is not specified, useradd uses the base directory specified by the HOME variable in /etc/default/useradd, or defaults to /home.
-c, --comment COMMENT    # Add a comment string. This is usually a short description of the login name and is used as the field for the user's full name.
-d, --home HOME_DIR      # The new user will be created using HOME_DIR as the value for the user's login directory.
-D, --defaults           # Change default settings.
-e, --expiredate EXPIRE_DATE # The date on which the user account will be disabled. The date is specified in YYYY-MM-DD format.
-f, --inactive INACTIVE      # The number of days after a password expires until the account is permanently disabled.
-g, --gid GROUP   # The group name or number of the user's initial login group. The group name must exist. The group number must refer to an already existing group.
-G, --groups GROUP1[,GROUP2,...[,GROUPN]]] # A list of supplementary groups which the user is also a member of. Each group is separated by a comma, with no intervening spaces.
-h, --help # Display help information and exit.
-k, --skel SKEL_DIR # The skeleton directory, which contains files and directories to be copied in the user's home directory, when the home directory is created by useradd.
-K, --key KEY=VALUE # Override /etc/login.defs defaults (UID_MIN, UID_MAX, UMASK, PASS_MAX_DAYS, etc.).
-l, --no-log-init   # Do not add the user to the lastlog and faillog databases.
-m, --create-home   # Create the user's home directory if it does not exist.
-M                  # Do not create the user's home directory, even if the system-wide setting in /etc/login.defs (CREATE_HOME) is set to yes.
-N, --no-user-group # Do not create a group with the same name as the user, but add the user to the group specified by the -g option or by the GROUP variable in /etc/default/useradd.
-o, --non-unique    # Allow the creation of a user account with a duplicate (non-unique) UID. This option is only valid when combined with the -u option.
-p, --password PASSWORD # The encrypted password, as returned by crypt(3). The default is to disable the password.
-r, --system        # Create a system account.
-s, --shell SHELL   # The name of the user's login shell.
-u, --uid UID       # The numerical value of the user's ID.
-U, --user-group    # Create a group with the same name as the user and add the user to that group.
-Z, --selinux-user SEUSER # The SELinux user for the user's login. Leaving this field blank defaults to the system's default SELinux user.

# Changing Defaults
# When called with only the -D option, useradd displays the current default values. When called with -D and other options, useradd updates the default values for the specified options. Valid default change options are:
```

### Parameters

Username: The username to be created.

### Exit Values

The `useradd` command exits with the following values:

```shell
0 Success
1 Cannot update password file
2 Invalid command syntax
3 Invalid argument to option
4 UID already in use (and no -o)
6 Specified group does not exist
9 Username already in use
10 Cannot update group file
12 Cannot create home directory
13 Cannot create mail spool
14 Cannot update SELinux user mapping
```

### Files

```shell
/etc/passwd # User account information.
/etc/shadow # Secure user account information.
/etc/group  # Group account information.
/etc/gshadow # Secure group account information.
/etc/default/useradd # Default values for account creation.
/etc/skel/   # Directory containing default files.
/etc/login.defs # Shadow password suite configuration.
```

### Examples

Create a new user and add to groups:

```shell
useradd –g sales jack –G company,employees    # -g: join primary group, -G: join supplementary groups
```

Create a new user account and set the ID:

```shell
useradd caojh -u 544
```

Note that when setting ID values, try to use values greater than 500 to avoid conflicts. Since Linux installations create some special users, values between 0 and 499 are usually reserved for system accounts like bin or mail.

Create a regular user:

```shell
useradd lutixia
```

Create a system user; system users are generally used for managing services and do not need to log in, so they are assigned nologin to restrict system access:

```shell
useradd -r -s /sbin/nologin mq
```

Modify the default parameters for creating users, setting the inactivity time after password expiration to 30 days:

```shell
useradd -D -f 30
```
