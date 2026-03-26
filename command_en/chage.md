chage
===

Change user password expiry information.

## Description

The **chage command** is used to modify the expiration dates of accounts and passwords.

### Syntax

```shell
chage [options] username
```

### Options

```shell
-m: The minimum number of days between password changes. A value of zero means the password can be changed at any time.
-M: The maximum number of days a password remains valid.
-w: The number of days before a password expires that a user will receive a warning message.
-E: The date on which the account will expire. After this date, the account will be unavailable.
-d: The date of the last password change.
-I: The inactivity period. If a password has been expired for this many days, the account will be unavailable.
-l: List the current settings. Used by non-privileged users to determine when their password or account expires.
```

### Examples

You can edit `/etc/login.defs` to set several parameters, and subsequent password settings will default to these values:

```shell
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_MIN_LEN    5
PASS_WARN_AGE   7
```

Alternatively, you can find the following two parameters in `/etc/default/useradd` to configure:

```shell
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

Modifying the configuration file affects newly created users, while for existing users, you should use `chage` directly.

Password policy information for the root account on my server:

```shell
chage -l root

Last password change					: Mar 12, 2013
Password expires					: never
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7
```

I can modify my password expiration time using the following command:

```shell
chage -M 60 root
chage -l root

Last password change					: Mar 12, 2013
Password expires					: May 11, 2013
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 60
Number of days of warning before password expires	: 9
```

Then, set the password inactivity period using the following command:

```shell
chage -I 5 root
chage -l root

Last password change					: Mar 12, 2013
Password expires					: May 11, 2013
Password inactive					: May 16, 2013
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 60
Number of days of warning before password expires	: 9
```

As seen from the above command, the password automatically becomes inactive 5 days after it expires, and the user will no longer be able to log in to the system.
