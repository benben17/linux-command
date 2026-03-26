ar
===

Create, modify, and extract from archives

## Additional Information

The **ar command** is a tool used to create or modify archive files, or extract files from archives. `ar` allows you to group multiple files into a single archive file. Within the archive, all member files retain their original attributes and permissions.

### Syntax

```shell
Usage: ar [emulation options] [-]{dmpqrstx}[abcDfilMNoOPsSTuvV] [--plugin <name>] [member-name] [count] archive-file file...
       ar -M [<mri-script]
```

### Options

> The following content is from GNU ar (GNU Binutils) version 2.40.

```shell
Commands:
      d            - Delete files from the archive
      m[ab]        - Move files within the archive
      p            - Print files found in the archive
      q[f]         - Quick append files to the archive
      r[ab][f][u]  - Replace existing files or insert new files into the archive
      s            - Act as ranlib
      t[O][v]      - Display contents of the archive
      x[o]         - Extract files from the archive
Specific Command Modifiers:
      [a]          - Place file after [member-name]
      [b]          - Place file before [member-name] (same as [i])
      [D]          - Use 0 for timestamps and uid/gid (default)
      [U]          - Use actual timestamps and uid/gid
      [N]          - Use instance [count] of name
      [f]          - Truncate inserted file names
      [P]          - Use full path names when matching
      [o]          - Preserve original dates
      [O]          - Display offsets of files in the archive
      [u]          - Only replace files that are newer than current archive contents
General Modifiers:
      [c]          - Do not warn if the library had to be created
      [s]          - Create an archive index (cf. ranlib)
      [l <text> ]  - Specify the dependencies of this library
      [S]          - Do not create a symbol table
      [T]          - Deprecated, use --thin instead
      [v]          - Be verbose
      [V]          - Display the version number
      @<file>      - Read options from <file>
      --target=BFDNAME - Specify the target object format as BFDNAME
      --output=DIRNAME - Specify the output directory for extraction operations
      --record-libdeps=<text> - Specify the dependencies of this library
      --thin       - Make a thin archive
Optional:
      --plugin <p> - Load the specified plugin
Emulation Options:
      No emulation-specific options
```

### Examples

Archive files:

```shell
[root@localhost ~]# ls   # Show files in the current directory
a.c	b.c d.c   install.log	  qte
anaconda-ks.cfg c.c Desktop 

[root@localhost ~]# ar rv one.bak a.c b.c  # Archive a.c and b.c
ar: creating one.bak
a - a.c
a - b.c
```

Archive multiple files:

```shell
[root@localhost ~]# ar rv two.bak *.c  # Archive all files ending in .c
ar: creating two.bak
a - a.c
a - b.c
a - c.c
a - d.c
```

Display the contents of the archive:

```shell
[root@localhost ~]# ar t two.bak    
a.c
b.c
c.c
d.c
```

Delete member files from an archive:

```shell
[root@localhost ~]# ar d two.bak a.c b.c c.c  
[root@localhost ~]# ar t two.bak       
d.c
```
