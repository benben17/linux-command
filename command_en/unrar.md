unrar
===

Decompress RAR files; extract files from RAR archives.

### Syntax

```shell
unrar [options] [switch commands] [filenames...] [path]
unrar <command> [-<switch 1> -<switch N>] archive [files...] [path...]
```

### Installation

In Linux, use the following commands to download and install:

```shell
wget https://www.rarlab.com/rar/rarlinux-6.0.2.tar.gz

cd ~/Downloads/
tar -zxvf rarlinux-6.0.2.tar.gz
```

### Options

```shell
e             # Extract compressed files to the current directory
l[t,b]        # List archive contents [technical information, bare]
p             # Print files to standard output
t             # Test archive files
v[t,b]        # Verbosely list archive contents [technical information, bare]
x             # Extract files with absolute paths
```

### Switches

Note: Each switch must be separated by a space. You cannot combine them.

```shell
-av-       # Disable authenticity verification check
-c-        # Disable comment display
-f         # Refresh files
-kb        # Keep broken extracted files
-ierr      # Send all messages to stderr
-inul      # Disable all messages
-o+        # Overwrite existing files
-o-        # Do not overwrite existing files
-p<password>
           # Set password
-p-        # Do not query for password
-r         # Recurse subdirectories
-u         # Update files
-v         # List all volumes
-x<file>
           # Exclude specified file
-x@<list>
           # Exclude files in specified list file
-x@        # Read filenames to exclude from stdin
-y         # Assume Yes on all queries
```

### Parameters

Directory: Specifies the directory to display, or specific files.

### Examples

Extract `test.rar` in the current directory with full paths:

```shell
unrar x test.rar
```

Extract `test.rar` in the current directory with full paths (as root):

```shell
[root@linux ~]# unrar x test.rar
```

View contents of the RAR package:

```shell
[root@linux ~]# unrar l test.rar
```

Test if the RAR package can be successfully decompressed:

```shell
[root@linux ~]# unrar t test.rar
```

Extract to the current folder:

```shell
[root@linux ~]# unrar e test.rar
```
