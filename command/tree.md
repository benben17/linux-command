tree
===

List directory contents in a tree-like format

## Description

The **tree command** lists the contents of a directory in a tree-like format.

### Syntax

```shell
tree [options] [parameters]
```

### Options

```shell
------- Listing Options -------
-a            # Display all files and directories (including hidden ones).
-d            # List directories only.
-l            # Follow symbolic links as if they were directories.
-f            # Print the full relative path for each file.
-x            # Stay on the current file system only.
-L level      # Max display depth of the directory tree.
-R            # Rerun tree when max dir level reached.
-P pattern    # List only those files that match the wildcard pattern.
-I pattern    # Do not list files that match the wildcard pattern.
--ignore-case # Ignore case when pattern matching.
--matchdirs   # Include directory names in -P pattern matching.
--noreport    # Turn off file/directory count at the end of the tree listing.
--charset X   # Use charset X for terminal/HTML and indentation line output.
--filelimit # # Do not descend directories with more than # files.
--timefmt <f> # Print and format time according to the format <f>.
-o filename   # Output to file instead of stdout.
-------- File Options ---------
-q            # Print non-printable characters as '?'.
-N            # Print non-printable characters as is.
-Q            # Quote filenames with double quotes.
-p            # Print permissions for each file.
-u            # Print the username, or UID if no username is available.
-g            # Print the group name, or GID if no group name is available.
-s            # Print the size of each file in bytes.
-h            # Print the size in a human-readable way (e.g., KB, MB).
--si          # Like -h, but use SI units (powers of 1000).
-D            # Print the date of the last modification.
-F            # Append a '/' for directories, '*' for executable files, '@' for symbolic links, '|' for FIFOs, and '=' for sockets.
--inodes      # Print inode number of each file.
--device      # Print device ID number to which each file belongs.
------- Sorting Options -------
-v            # Sort files alphanumerically by version.
-t            # Sort files by last modification time.
-c            # Sort files by last status change time.
-U            # Leave files unsorted.
-r            # Reverse the order of the sort.
--dirsfirst   # List directories before files (-U disables).
--sort X      # Select sort: name, version, size, mtime, ctime.
------- Graphics Options ------
-i            # Do not print indentation lines.
-A            # Use ANSI line graphics characters.
-S            # Print with CP437 (console) graphics indentation lines.
-n            # Turn off colorization (overridden by -C).
-C            # Turn on colorization.
------- XML / HTML / JSON Options -------
-X            # Print out an XML representation of the tree.
-J            # Print out a JSON representation of the tree.
-H baseHREF   # Print out HTML format with baseHREF as top directory.
-T string     # Replace the default HTML title and H1 header with string.
--nolinks     # Turn off hyperlinks in HTML output.
---- Miscellaneous Options ----
--version     # Display version information.
--help        # Display usage help information.
--            # Options processing terminator.
```

### Parameters

Directory: Execute the tree command on the specified directory, listing all files and subdirectories.

### Examples

List filenames in the first level of the `/private/` directory:

```shell
tree /private/ -L 1
/private/
├── etc
├── tftpboot
├── tmp
└── var
```

Ignore folders:

```shell
tree -I node_modules # Ignore node_modules in the current directory
tree -P node_modules # List the structure of the node_modules folder in the current directory
tree -P node_modules -L 2 # Display two levels of the node_modules directory
tree -L 2 > /home/www/tree.txt # Save the current directory structure to tree.txt
```

Ignore multiple folders:

```shell
tree -I 'node_modules|icon|font' -L 2
```

List all files in `/private/` in a non-tree format:

```
tree -if /private/
/private
/private/a1
/private/a2
/private/etc
/private/etc/b1
/private/etc/b2
/private/tftpboot
```

Show all files and directories (including hidden ones), ignore `node_modules` and `.git`, and display two levels (`-L 2`).

```shell
$ tree -I 'node_modules|.git' -L 2 -a

.
├── .github
│   └── workflows
├── LICENSE
├── README.md
└── renovate.json
```
