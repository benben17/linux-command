lastlog
===

Display the most recent login information for all users in the system

## Description

The **lastlog** command is used to display the most recent login information for all users in the system.

The `lastlog` file is queried every time a user logs in. You can use the `lastlog` command to check when a specific user last logged in, and format the output of the `/var/log/lastlog` file. It displays the login name, port (tty), and the last login time, sorted by UID. If a user has never logged in, `lastlog` displays `**Never logged in**`. Note that this command usually needs to be run as root.

### Syntax

```shell
lastlog (options)
```

### Options

```shell
-b <days>: Display login information from more than the specified number of days ago;
-h: Display help information;
-t <days>: Display login information from within the specified number of days;
-u <username>: Display the most recent login information for the specified user.
```

### Examples

```shell
lastlog
Username         Port     From             Latest
root             pts/0    221.6.45.34      Tue Dec 17 09:40:48 +0800 2013
bin                                         **Never logged in** 
daemon                                      **Never logged in** 
adm                                         **Never logged in** 
lp                                          **Never logged in** 
sync                                        **Never logged in** 
shutdown                                    **Never logged in** 
halt                                        **Never logged in** 
mail                                        **Never logged in** 
news                                        **Never logged in** 
uucp                                        **Never logged in** 
operator                                    **Never logged in** 
games                                       **Never logged in** 
gopher                                      **Never logged in** 
ftp                                         **Never logged in** 
nobody                                      **Never logged in** 
vcsa                                        **Never logged in** 
ntp                                         **Never logged in** 
sshd                                        **Never logged in** 
nscd                                        **Never logged in** 
ldap                                        **Never logged in** 
postfix                                     **Never logged in** 
www                                         **Never logged in** 
mysql                                       **Never logged in** 
```
