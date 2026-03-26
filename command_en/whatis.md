whatis
===

Display one-line manual page descriptions

## Description

The **whatis command** searches the manual page names and descriptions for the given command and prints the result to the terminal.

The command searches a database created by `mandb` (or `catman -w` on older systems) for the command name, system call, library function, or special filename. It displays the header line of the manual page, which typically contains a one-line description. This is equivalent to running `man -f`.

### Syntax

```shell
whatis [command]
```

### Examples

```shell
[root@localhost ~]# whatis ls
ls                   (1)  - list directory contents
ls                   (1p)  - list directory contents

[root@localhost ~]# whatis cp
cp                   (1)  - copy files and directories
cp                   (1p)  - copy files

[root@localhost ~]# whatis chown
chown                (1)  - change file owner and group
chown                (1p)  - change the file ownership
chown                (2)  - change ownership of a file
chown                (3p)  - change owner and group of a file

[root@localhost ~]# whatis man
man                  (1)  - format and display the on-line manual pages
man                  (1p)  - display system documentation
man                  (7)  - macros to format man pages
man                 (rpm) - A set of documentation tools: man, apropos and whatis.
man-pages           (rpm) - Man (manual) pages from the Linux Documentation Project.
man.config [man]     (5)  - configuration data for man
```
