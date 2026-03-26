chfn
===

Used to change the information displayed by the finger command

## Description

The **chfn command** is used to change the information displayed by the finger command. This information is stored in the `/etc/passwd` file. If no options are specified, the `chfn` command will enter an interactive mode.

### Syntax

```shell
chfn [options] [arguments]
```

### Options

```shell
-f <full_name> or --full-name <full_name>: Set the full name;
-h <home_phone> or --home-phone <home_phone>: Set the home phone number;
-o <office_address> or --office <office_address>: Set the office address;
-p <office_phone> or --office-phone <office_phone>: Set the office phone number;
-u or --help: Online help;
-v or --version: Display version information.
```

### Arguments

Username: Specify the username for which the finger information should be changed.

### Examples

Example 1: Change finger information:

```shell
[root@localhost Desktop]# chfn
Changing finger information for root.
Name [root]: jack
Office []: hn
Office Phone []: 888888
Home Phone []: 9999999

Finger information changed.
```

Example 2: Change account full name:

```shell
[root@localhost Desktop]# chfn -f jack
Changing finger information for root.
Finger information changed.
```

Example 3:

```shell
shell>> chfn
Changing finger information for user
Password: [del]
Name[]:linuxde ### Information provided for finger
Office[]:NCCU
Office Phone[]: [del]
Home Phone[]: [del]
```
