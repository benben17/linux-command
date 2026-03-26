column
===

Formats output into columns

## Synopsis

```shell
column [options] [file ...]
```

## Main Purpose

- Format single-column data into multiple columns, with a specified line width and automatic wrapping.
- Quickly organize multi-column data by aligning characters in each column.

## Arguments

file (optional): If no file is specified, it reads from standard input, making it compatible with pipes.

## Options

```shell
-c, --columns <width>           Output width in characters.
-t, --table                     Create a table (aligning characters in each column).
-s, --separator <string>        Specify the delimiter for table recognition.
-o, --output-separator <string> Specify the column separator for the output table (default is two spaces).
-x, --fillrows                  Fill rows before columns.
-N, --table-columns <names>     Add column names (comma-separated).
-J  --json                      Format output as JSON (requires -N/--table-columns).
-h, --help                      Display help.
-V, --version                   Output version information.
```

## Return Value

The formatted string.

## Examples

- Organizing single-column data:

```shell
# Generate 26 English letters, one per line.
$ for a in {a..z}; do echo $a; done > test

# Maximum 60 characters per line.
$ cat test | column -c 60
a       e       i       m       q       u       y
b       f       j       n       r       v       z
c       g       k       o       s       w
d       h       l       p       t       x

# Further organize with a default column width separator of two spaces.
$ cat test | column -c 60 | column -t
a  e  i  m  q  u  y
b  f  j  n  r  v  z
c  g  k  o  s  w
d  h  l  p  t  x

# Specify ', ' as the column separator.
$ cat test | column -c 60 | column -t -o ', '
a, e, i, m, q, u, y
b, f, j, n, r, v, z
c, g, k, o, s, w
d, h, l, p, t, x
```

- Organizing multi-column data:

```shell
# A disorganized text file named 'test'.
$ cat test
Address[0] Metal3,pin 133.175:159.92
Address[1] Metal3,pin 112.38:159.92
Address[2] Metal3,pin 70.775:159.92
Address[3] Metal3,pin 41.655:159.92
DataIn[0] Metal3,pin 66.615:159.92
DataIn[1] Metal3,pin 37.495:159.92
DataIn[2] Metal3,pin 122.88:159.92
DataIn[3] Metal3,pin 95.74:159.92
DataOut[0] Metal3,pin 45.815:159.92
DataOut[1] Metal3,pin 79.095:159.92
DataOut[2] Metal3,pin 104.055:159.92
DataOut[3] Metal3,pin 62.46:159.92
MemReq Metal3,pin 108.215:159.92
RdWrBar Metal3,pin 87.415:159.92
clock Metal3,pin 74.935:159.92

# Align columns.
$ cat test | column -t
Address[0]  Metal3,pin  133.175:159.92
Address[1]  Metal3,pin  112.38:159.92
Address[2]  Metal3,pin  70.775:159.92
Address[3]  Metal3,pin  41.655:159.92
DataIn[0]   Metal3,pin  66.615:159.92
DataIn[1]   Metal3,pin  37.495:159.92
DataIn[2]   Metal3,pin  122.88:159.92
DataIn[3]   Metal3,pin  95.74:159.92
DataOut[0]  Metal3,pin  45.815:159.92
DataOut[1]  Metal3,pin  79.095:159.92
DataOut[2]  Metal3,pin  104.055:159.92
DataOut[3]  Metal3,pin  62.46:159.92
MemReq      Metal3,pin  108.215:159.92
RdWrBar     Metal3,pin  87.415:159.92
clock       Metal3,pin  74.935:159.92

# Recognize ',' and ':' as separators as well.
$ cat test | column -t -s ',: '
Address[0]  Metal3  pin  133.175  159.92
Address[1]  Metal3  pin  112.38   159.92
Address[2]  Metal3  pin  70.775   159.92
Address[3]  Metal3  pin  41.655   159.92
DataIn[0]   Metal3  pin  66.615   159.92
DataIn[1]   Metal3  pin  37.495   159.92
DataIn[2]   Metal3  pin  122.88   159.92
DataIn[3]   Metal3  pin  95.74    159.92
DataOut[0]  Metal3  pin  45.815   159.92
DataOut[1]  Metal3  pin  79.095   159.92
DataOut[2]  Metal3  pin  104.055  159.92
DataOut[3]  Metal3  pin  62.46    159.92
MemReq      Metal3  pin  108.215  159.92
RdWrBar     Metal3  pin  87.415   159.92
clock       Metal3  pin  74.935   159.92
```

- Add column names and output in JSON format:

```shell
$ column -J -s ":" -N "Username,Password,UID,GID,Gecos,HomeDirectory,Shell" /etc/passwd
{
   "table": [
      {
         "username": "root",
         "password": "x",
         "uid": "0",
         "gid": "0",
         "gecos": "root",
         "homedirectory": "/root",
         "shell": "/bin/bash"
      },{
         "username": "daemon",
         "password": "x",
         "uid": "1",
         "gid": "1",
         "gecos": "daemon",
         "homedirectory": "/usr/sbin",
         "shell": "/usr/sbin/nologin"
      },{
         "username": "bin",
         "password": "x",
         "uid": "2",
         "gid": "2",
         "gecos": "bin",
         "homedirectory": "/bin",
         "shell": "/usr/sbin/nologin"
      },{
         "username": "sys",
         "password": "x",
         "uid": "3",
         "gid": "3",
         "gecos": "sys",
         "homedirectory": "/dev",
         "shell": "/usr/sbin/nologin"
      },{
         "username": "sync",
         "password": "x",
         "uid": "4",
         "gid": "65534",
         "gecos": "sync",
         "homedirectory": "/bin",
         "shell": "/bin/sync"
      }
   ]
}
```
