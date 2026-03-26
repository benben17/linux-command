getfacl
===

Get file access control lists (ACLs).

## Supplemental Information

For each file, `getfacl` displays the file name, owner, group, and the Access Control List (ACL). If a directory has a default ACL, `getfacl` also displays it. Non-directories cannot have default ACLs.
If `getfacl` is used on a file system that does not support ACLs, it displays the access permissions defined by the traditional file mode permission bits. See also `setfacl`.

### Options

```shell
-a, --access              # Display the file access control list.
-d, --default             # Display the default access control list.
-c, --omit-header         # Do not display the comment header (the first three lines of output for each file).
-e, --all-effective       # Print all effective rights comments, even if identical to the rights defined by the ACL entry.
-E, --no-effective        # Do not print effective rights comments.
-s, --skip-base           # Skip files that only have the base ACL entries (owner, group, others).
-R, --recursive           # List ACLs of all files and directories recursively.
-L, --logical             # Logical walk, follow symbolic links to directories. The default behavior is to follow symbolic link arguments, and skip symbolic links encountered in subdirectories. Only effective in combination with -R.
-P, --physical            # Physical walk, do not follow symbolic links to directories. This also skips symbolic link arguments. Only effective in combination with -R.
-t, --tabular             # Use an alternative tabular output format. The ACL and the default ACL are displayed side by side. Permissions that are ineffective due to the ACL mask entry are displayed in uppercase. The entry tag names for ACL_USER_OBJ and ACL_GROUP_OBJ entries are also displayed in uppercase, which helps in identifying these entries.
-p, --absolute-names      # Do not strip leading slash characters ('/'). The default behavior is to strip leading slash characters.
-n, --numeric             # List numeric user and group IDs.
-v, --version             # Print the version of getfacl and exit.
-h, --help                # Print help explaining the command line options.
--                        # End of command line options. All remaining arguments are interpreted as file names, even if they start with a dash character.
-                         # If the file name argument is a single dash character, getfacl reads the list of files from standard input.
```

### Examples

The `getfacl` command displays the file access control list by default. Open a terminal and enter the following command:

```shell
getfacl tmp 

# file: tmp
# owner: zdx
# group: zdx
# flags: -s-
user::rwx
group::rwx
other::r-x
default:user::rwx
default:group::rwx
default:other::r-x
```
