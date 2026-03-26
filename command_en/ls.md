ls
===

List directory contents

## Description

The **ls command** is short for "list". It is used to display a list of files and directories and is one of the most frequently used commands in Linux. The output of the `ls` command can be displayed with color highlighting to distinguish between different types of files.

### Syntax

```shell
ls [OPTION]... [FILE]...
   [-1abcdfgiklmnopqrstuxABCDFGLNQRSUX] [-w cols] [-T cols] [-I pattern] [--full-time] 
   [--format={long,verbose,commas,across,vertical,single-column}] 
   [--sort={none,time,size,extension}] [--time={atime,access,use,ctime,status}] 
   [--color[={none,auto,always}]] [--help] [--version] [--]
```

### Options

```shell
-C     # List entries by columns, sorted vertically.
-F     # Append indicator (one of */=>@|) to entries.
-R     # List subdirectories recursively.
-a     # Do not ignore entries starting with ".".
-c     # With -lt: sort by, and show, ctime (time of last modification of file status information); with -l: show ctime and sort by name; otherwise: sort by ctime.
-d     # List directories themselves, not their contents.
-i     # Print the index number (inode) of each file.
-l     # Use a long listing format.
-q     # Print ? instead of nongraphic characters.
-r     # Reverse order while sorting.
-t     # Sort by modification time, newest first.
-u     # With -lt: sort by, and show, access time; with -l: show access time and sort by name; otherwise: sort by access time.
-1     # List one file per line.
-1, --format=single-column  # List one file per line. This is the default when standard output is not a terminal.
-a, --all # List all files in the directory, including those starting with ".".
-b, --escape # Print C-style escapes for nongraphic characters.
-c, --time=ctime, --time=status
      # Sort by and show ctime (time of last status change). If using long format (-l), use status change time instead of modification time.
-d, --directory
      # List directory names like other files, rather than listing their contents.
-f    # Do not sort; list entries in directory order. Enables -a, disables -l, --color, and -s if they appeared before -f.
-g    # Like -l, but do not list owner.
-i, --inode
      # Print the index number of each file (also called the file serial number and index number).
-k, --kilobytes
      # Default to 1024-byte blocks for disk usage; used with -s and for directory totals.
-l, --format=long, --format=verbose
      # Use a long listing format. Information includes file mode, number of links, owner name, group name, size in bytes, and timestamp.
      # For files older than 6 months or more than 1 hour into the future, the time includes the year instead of the time of day.
      # A total block count is listed before each directory.

# Permissions are listed similar to symbolic mode. ls combines multiple bits in the third character of each set:
      # s: setuid or setgid is set, and the corresponding execute bit is set.
      # S: setuid or setgid is set, but the corresponding execute bit is not set.
      # t: sticky bit is set, and the corresponding execute bit is set.
      # T: sticky bit is set, but the corresponding execute bit is not set.
      # x: execute bit is set, but none of the above apply.
      # -: execute bit is not set.

-m, --format=commas
      # Fill width with a comma separated list of entries.
-n, --numeric-uid-gid
      # List numeric user and group IDs instead of names.
-o    # Like -l, but do not list group information.
-p    # Append / indicator to directories.
-q, --hide-control-chars
      # Print ? instead of non-graphic characters.
-r, --reverse
      # Reverse order while sorting.
-s, --size
      # Print the allocated size of each file, in blocks.
-t, --sort=time
      # Sort by modification time, newest first.
-u, --time=atime, --time=access, --time=use
      # Sort by and show access time.
-w, --width cols
       # Assume screen width is 'cols' columns.

-x, --format=across, --format=horizontal
       # List entries by lines instead of by columns.

-A, --almost-all
       # Do not list implied . and ..

-B, --ignore-backups
       # Do not list implied entries ending with ~.

-C, --format=vertical
       # List entries by columns. This is the default if standard output is a terminal.

-D, --dired
       # Generate output designed for Emacs' dired mode.

-F, --classify, --file-type
       # Append indicator (one of */=>@|) to entries.

-G, --no-group
       # In a long listing, don't print group names.

-I, --ignore=PATTERN
       # Do not list implied entries matching shell PATTERN.

-L, --dereference
       # When showing file information for a symbolic link, show information for the file the link references rather than for the link itself.

-N, --literal
       # Print raw entry names (don't treat control characters specially).

-Q, --quote-name
       # Enclose entry names in double quotes.

-R, --recursive
       # List subdirectories recursively.

-S, --sort=size
       # Sort by file size, largest first.

-T, --tabsize=COLS
       # Assume tab stops at each COLS instead of 8.

-U, --sort=none
       # Do not sort; list entries in directory order.

-X, --sort=extension
       # Sort alphabetically by entry extension.

--color[=WHEN]
       # Colorize the output. WHEN can be 'always' (default), 'auto', or 'never'.

--full-time
       # Like -l --time-style=full-iso.
```

### Parameters

Directory: The directory or files to list.

### Examples

```shell
$ ls       # List visible files in the current directory
$ ls -l    # List detailed information of visible files
$ ls -hl   # List detailed information with human-readable file sizes
$ ls -al   # List detailed information of all files (including hidden)
$ ls --human-readable --size -1 -S --classify # Sort by file size
$ du -sh * | sort -h # Sort by file size (alternative)
```

List all files including hidden ones:

```shell
[root@localhost ~]# ls -a
.   anaconda-ks.cfg  .bash_logout   .bashrc  install.log         .mysql_history  satools  .tcshrc   .vimrc
..  .bash_history    .bash_profile  .cshrc   install.log.syslog  .rnd            .ssh     .viminfo
```

Output long format:

```shell
[root@localhost ~]# ls -1

anaconda-ks.cfg
install.log
install.log.syslog
satools
```

Show file inode information:

```shell
[root@localhost ~]# ls -i -l anaconda-ks.cfg install.log
2345481 -rw------- 1 root root   859 Jun 11 22:49 anaconda-ks.cfg
2345474 -rw-r--r-- 1 root root 13837 Jun 11 22:49 install.log
```

Horizontal output:

```shell
[root@localhost /]# ls -m

bin, boot, data, dev, etc, home, lib, lost+found, media, misc, mnt, opt, proc, root, sbin, selinux, srv, sys, tmp, usr, var
```

Sort by last modification time (newest first):

```shell
[root@localhost /]# ls -t

tmp  root  etc  dev  lib  boot  sys  proc  data  home  bin  sbin  usr  var  lost+found  media  mnt  opt  selinux  srv  misc
```

Recursive listing:

```shell
[root@localhost ~]# ls -R
.:
anaconda-ks.cfg  install.log  install.log.syslog  satools

./satools:
black.txt  freemem.sh  iptables.sh  lnmp.sh  mysql  php502_check.sh  ssh_safe.sh
```

Print UID and GID:

```shell
[root@localhost /]# ls -n

total 254
drwxr-xr-x   2 0 0  4096 Jun 12 04:03 bin
drwxr-xr-x   4 0 0  1024 Jun 15 14:45 boot
drwxr-xr-x   6 0 0  4096 Jun 12 10:26 data
drwxr-xr-x  10 0 0  3520 Sep 26 15:38 dev
drwxr-xr-x  75 0 0  4096 Oct 16 04:02 etc
drwxr-xr-x   4 0 0  4096 Jun 12 10:26 home
drwxr-xr-x  14 0 0 12288 Jun 16 04:02 lib
drwx------   2 0 0 16384 Jun 11 22:46 lost+found
drwxr-xr-x   2 0 0  4096 May 11  2011 media
drwxr-xr-x   2 0 0  4096 Nov  8  2010 misc
drwxr-xr-x   2 0 0  4096 May 11  2011 mnt
drwxr-xr-x   2 0 0  4096 May 11  2011 opt
dr-xr-xr-x 232 0 0     0 Jun 15 11:04 proc
drwxr-x---   4 0 0  4096 Oct 15 14:43 root
drwxr-xr-x   2 0 0 12288 Jun 12 04:03 sbin
drwxr-xr-x   2 0 0  4096 May 11  2011 selinux
drwxr-xr-x   2 0 0  4096 May 11  2011 srv
drwxr-xr-x  11 0 0     0 Jun 15 11:04 sys
drwxrwxrwt   3 0 0 98304 Oct 16 08:45 tmp
drwxr-xr-x  13 0 0  4096 Jun 11 23:38 usr
drwxr-xr-x  19 0 0  4096 Jun 11 23:38 var
```

List detailed information:

```shell
[root@localhost /]# ls -l

total 254
drwxr-xr-x   2 root root  4096 Jun 12 04:03 bin
drwxr-xr-x   4 root root  1024 Jun 15 14:45 boot
drwxr-xr-x   6 root root  4096 Jun 12 10:26 data
drwxr-xr-x  10 root root  3520 Sep 26 15:38 dev
drwxr-xr-x  75 root root  4096 Oct 16 04:02 etc
drwxr-xr-x   4 root root  4096 Jun 12 10:26 home
drwxr-xr-x  14 root root 12288 Jun 16 04:02 lib
drwx------   2 root root 16384 Jun 11 22:46 lost+found
drwxr-xr-x   2 root root  4096 May 11  2011 media
drwxr-xr-x   2 root root  4096 Nov  8  2010 misc
drwxr-xr-x   2 root root  4096 May 11  2011 mnt
drwxr-xr-x   2 root root  4096 May 11  2011 opt
dr-xr-xr-x 232 root root     0 Jun 15 11:04 proc
drwxr-x---   4 root root  4096 Oct 15 14:43 root
drwxr-xr-x   2 root root 12288 Jun 12 04:03 sbin
drwxr-xr-x   2 root root  4096 May 11  2011 selinux
drwxr-xr-x   2 root root  4096 May 11  2011 srv
drwxr-xr-x  11 root root     0 Jun 15 11:04 sys
drwxrwxrwt   3 root root 98304 Oct 16 08:48 tmp
drwxr-xr-x  13 root root  4096 Jun 11 23:38 usr
drwxr-xr-x  19 root root  4096 Jun 11 23:38 var
```

List detailed information with human-readable sizes:

```shell
[root@localhost /]# ls -lh

total 254K
drwxr-xr-x   2 root root 4.0K Jun 12 04:03 bin
drwxr-xr-x   4 root root 1.0K Jun 15 14:45 boot
drwxr-xr-x   6 root root 4.0K Jun 12 10:26 data
drwxr-xr-x  10 root root 3.5K Sep 26 15:38 dev
drwxr-xr-x  75 root root 4.0K Oct 16 04:02 etc
drwxr-xr-x   4 root root 4.0K Jun 12 10:26 home
drwxr-xr-x  14 root root  12K Jun 16 04:02 lib
drwx------   2 root root  16K Jun 11 22:46 lost+found
drwxr-xr-x   2 root root 4.0K May 11  2011 media
drwxr-xr-x   2 root root 4.0K Nov  8  2010 misc
drwxr-xr-x   2 root root 4.0K May 11  2011 mnt
drwxr-xr-x   2 root root 4.0K May 11  2011 opt
dr-xr-xr-x 235 root root    0 Jun 15 11:04 proc
drwxr-x---   4 root root 4.0K Oct 15 14:43 root
drwxr-xr-x   2 root root  12K Jun 12 04:03 sbin
drwxr-xr-x   2 root root 4.0K May 11  2011 selinux
drwxr-xr-x   2 root root 4.0K May 11  2011 srv
drwxr-xr-x  11 root root    0 Jun 15 11:04 sys
drwxrwxrwt   3 root root  96K Oct 16 08:49 tmp
drwxr-xr-x  13 root root 4.0K Jun 11 23:38 usr
drwxr-xr-x  19 root root 4.0K Jun 11 23:38 var
```

Show directory information:

```shell
[root@localhost /]# ls -ld /etc/

drwxr-xr-x 75 root root 4096 Oct 16 04:02 /etc/
```

Sort by time, detailed information:

```shell
[root@localhost /]# ls -lt

total 254
drwxrwxrwt   3 root root 98304 Oct 16 08:53 tmp
drwxr-xr-x  75 root root  4096 Oct 16 04:02 etc
drwxr-x---   4 root root  4096 Oct 15 14:43 root
drwxr-xr-x  10 root root  3520 Sep 26 15:38 dev
drwxr-xr-x  14 root root 12288 Jun 16 04:02 lib
drwxr-xr-x   4 root root  1024 Jun 15 14:45 boot
drwxr-xr-x  11 root root     0 Jun 15 11:04 sys
dr-xr-xr-x 232 root root     0 Jun 15 11:04 proc
drwxr-xr-x   6 root root  4096 Jun 12 10:26 data
drwxr-xr-x   4 root root  4096 Jun 12 10:26 home
drwxr-xr-x   2 root root  4096 Jun 12 04:03 bin
drwxr-xr-x   2 root root 12288 Jun 12 04:03 sbin
drwxr-xr-x  13 root root  4096 Jun 11 23:38 usr
drwxr-xr-x  19 root root  4096 Jun 11 23:38 var
drwx------   2 root root 16384 Jun 11 22:46 lost+found
drwxr-xr-x   2 root root  4096 May 11  2011 media
drwxr-xr-x   2 root root  4096 May 11  2011 mnt
drwxr-xr-x   2 root root  4096 May 11  2011 opt
drwxr-xr-x   2 root root  4096 May 11  2011 selinux
drwxr-xr-x   2 root root  4096 May 11  2011 srv
drwxr-xr-x   2 root root  4096 Nov  8  2010 misc
```

Sort by modification time in reverse:

```shell
[root@localhost /]# ls -ltr

total 254
drwxr-xr-x   2 root root  4096 Nov  8  2010 misc
drwxr-xr-x   2 root root  4096 May 11  2011 srv
drwxr-xr-x   2 root root  4096 May 11  2011 selinux
drwxr-xr-x   2 root root  4096 May 11  2011 opt
drwxr-xr-x   2 root root  4096 May 11  2011 mnt
drwxr-xr-x   2 root root  4096 May 11  2011 media
drwx------   2 root root 16384 Jun 11 22:46 lost+found
drwxr-xr-x  19 root root  4096 Jun 11 23:38 var
drwxr-xr-x  13 root root  4096 Jun 11 23:38 usr
drwxr-xr-x   2 root root 12288 Jun 12 04:03 sbin
drwxr-xr-x   2 root root  4096 Jun 12 04:03 bin
drwxr-xr-x   4 root root  4096 Jun 12 10:26 home
drwxr-xr-x   6 root root  4096 Jun 12 10:26 data
dr-xr-xr-x 232 root root     0 Jun 15 11:04 proc
drwxr-xr-x  11 root root     0 Jun 15 11:04 sys
drwxr-xr-x   4 root root  1024 Jun 15 14:45 boot
drwxr-xr-x  14 root root 12288 Jun 16 04:02 lib
drwxr-xr-x  10 root root  3520 Sep 26 15:38 dev
drwxr-x---   4 root root  4096 Oct 15 14:43 root
drwxr-xr-x  75 root root  4096 Oct 16 04:02 etc
drwxrwxrwt   3 root root 98304 Oct 16 08:54 tmp
```

Classify files with indicators:

```shell
[root@localhost nginx-1.2.1]# ls -F

auto/  CHANGES  CHANGES.ru  conf/  configure*  contrib/  html/  LICENSE  Makefile  man/  objs/  README  src/
```

List files with color:

```shell
[root@localhost nginx-1.2.1]# ls --color=auto

auto  CHANGES  CHANGES.ru  conf  configure  contrib  html  LICENSE  Makefile  man  objs  README  src
```

## Extra Knowledge

### File types represented by different colors

* `Blue`<!--rehype:style=background: blue;color:white;-->: Directory
* `Green`<!--rehype:style=background: green;color:white;-->: Executable file
* `White`<!--rehype:style=background: #efefef;-->: General file (e.g., text, configuration)
* `Red`<!--rehype:style=background: red;color:white;-->: Compressed or archive file
* `Light Blue`<!--rehype:style=background: #c4c3ff;-->: Symbolic link
* Flashing Red: Problem with symbolic link
* Yellow: Device file
* Cyan: Pipe (FIFO)
