find
===

Search for files in a directory hierarchy.

## Explanation

Starting from each specified starting point (directory), search the directory tree rooted at that point, evaluating the given expression from **left to right** according to operator precedence rules until the result is determined, at which point `find` moves on to the next filename.

## Description

The options listed in this document refer to **options in the expression list**. These options control the behavior of `find` and must be specified immediately **after the last path name**.

There are five "real" options: `-H, -L, -P, -D, and -O`. If present, they **must appear before the first path name**. This section does not describe those; for more details, refer to the [find man page on man7.org](https://man7.org/linux/man-pages/man1/find.1.html#top_of_page).

If no parameters are provided, the `find` command searches for subdirectories and files in the current directory and displays them all. This is equivalent to:
```shell
find . -print
```

## Syntax

```shell
find [-H] [-L] [-P] [-D debugopts] [-Olevel] [starting-point...] [expression]
```

Excluding real options (more common):
```shell
find [starting-point...] [expression]
```

## Expression Categories
The part after the starting points (list) is the expression. This is a **query specification** describing how we match files (returning **true** or **false**) and what actions to perform on the matched files. An expression consists of a series of elements:
- Tests: Tests return a true or false value, usually based on some property of the file being considered. For example, the `-empty` test is true only if the current file is empty.
- Actions: Actions have side effects (such as printing to standard output) and return true or false, usually based on whether they were successful. For example, the `-print` action prints the name of the current file to standard output.
- Global Options: Global options affect the execution of tests and actions specified in any part of the command line. Global options always return true. For example, the `-depth` option causes `find` to traverse the filesystem in a depth-first order.
- Positional Options: Positional options affect only subsequent tests or actions. Positional options always return true. For example, the `-regextype` option is a positional option used to specify the regular expression dialect used by subsequent regular expressions in the command line.
- Operators: Operators connect other items in the expression. They include `-o` (logical OR) and `-a` (logical AND). If no operator is specified, `-a` is used by default.

## Expression Options

### Tests
```shell
-amin <minutes>: Find files or directories accessed exactly <minutes> ago.
-anewer <reference-file>: Find files or directories whose access time is more recent than the access time of the specified reference file or directory.
-atime <n-24-hour-periods>: Find files or directories accessed exactly n*24 hours ago.
-cmin <minutes>: Find files or directories changed exactly <minutes> ago.
-cnewer <reference-file>: Find files or directories whose status change time is more recent than the status change time of the specified reference file or directory.
-ctime <n-24-hour-periods>: Find files or directories changed exactly n*24 hours ago.
-empty: Find files with a size of 0 bytes, or empty directories.
-executable: Match files that are executable and directories that are searchable by the current user.
-false: Always return false.
-fstype <type>: Search only on filesystems of the specified type.
-gid <gid>: Find files or directories with the specified group ID.
-group <group-name>: Find files or directories belonging to the specified group name.
-ilname <pattern>: Like -lname, but case-insensitive.
-iname <pattern>: Like -name, but case-insensitive.
-inum <inode-number>: Find files or directories with the specified inode number.
-ipath <pattern>: Like -path, but case-insensitive.
-iregex <pattern>: Like -regex, but case-insensitive.
-iwholename <pattern>: See -ipath. This option is less portable than -ipath.
-links <n>: Find files or directories with exactly <n> hard links.
-lname <pattern>: Find symbolic links whose target matches the specified pattern.
-mmin <minutes>: Find files or directories modified exactly <minutes> ago.
-mtime <n-24-hour-periods>: Find files or directories modified exactly n*24 hours ago.
-name <pattern>: Find files or directories matching the specified pattern.
-newer <reference-file>: Find files or directories whose modification time is more recent than the modification time of the specified reference file.
-newerXY <reference>: Succeeds if the timestamp 'X' of the file being considered is newer than the timestamp 'Y' of the reference file.
-nogroup: Find files or directories that do not belong to a valid group ID on the local system.
-nouser: Find files or directories that do not belong to a valid user ID on the local system.
-path <pattern>: Match the full file path against the specified pattern.
-perm <mode>: Find files or directories with the specified permissions.
-readable: Match files readable by the current user.
-regex <pattern>: Match the full file path against a regular expression.
-samefile <name>: Match files that point to the same inode as <name>.
-size <n>: Find files of the specified size.
-type <type>: Find files of the specified type.
-uid <uid>: Find files or directories with the specified user ID.
-used <days>: Find files or directories accessed <days> after their status was last changed.
-user <username>: Find files or directories belonging to the specified user.
-writable: Match files writable by the current user.
-xtype <type>: Like -type, but checks the type of the file pointed to by a symbolic link.
-context <pattern>: SELinux only. Match the file's security context against a glob pattern.
```

### Actions

#### -delete Delete files or directories.
> :warning: Warning: Since find parses the command line as an expression, putting `-delete` first will **delete everything** under the specified starting point. Furthermore, `-delete` cannot delete a directory unless it is empty.

##### *No Parameters*

##### Description
Returns true if the deletion was successful. If the deletion fails, an error message is displayed, and find will exit with a non-zero status code.

##### Related Options
- **-depth**: Using the `-delete` action automatically enables the `-depth` option. To avoid unexpected behavior, it is usually better to **explicitly use** the `-depth` option earlier in the **Tests**.
- **-prune**: Since `-depth` invalidates `-prune`, the `-delete` action cannot be effectively combined with `-prune`. It is generally advisable to test the find command line with `-print` before adding `-delete` to perform the actual deletion.
- **-ignore_readdir_race**: When used with this option, find will ignore errors from the `-delete` action if the file has disappeared since the parent directory was read: it will not output an error diagnostic, will not change the exit code to non-zero, and the return code of the `-delete` action will be true.

#### -exec Execute a command

> :warning: Warning: There are unavoidable security issues with using the `-exec` action; the `-execdir` option should be used instead.

##### Parameters
`command ;` or `command {} +`

##### Description
The result is true if the return status is 0. **Note**: find treats **all subsequent arguments** as arguments to the `command` until it encounters an argument containing `;`. The string `{}` is replaced by the current file name being processed everywhere it occurs in the arguments to the `command`, not just in arguments where it stands alone, unlike some versions of find. Both constructions may need to be escaped with a backslash `\` or quoted to prevent expansion by the shell. The specified command is run once for each matched file. The command is executed in the starting directory.

#### -execdir Execute a command in the subdirectory containing the matched file

##### Parameters
`command ;` | `command {} +`

##### Description
Similar to `-exec`, but the specified `command` is **run in the subdirectory** containing the matched file, rather than find's starting directory. As with `-exec`, `{}` should be quoted if calling find from a shell. This is a more secure way to invoke `command` as it avoids race conditions during path resolution. Like the `-exec` action, the `+` form of `-execdir` builds a command line to process multiple matched files, but any given `command` invocation will only list files that exist in the same subdirectory. If using this option, ensure the PATH environment variable does not refer to `.`, otherwise an attacker could run any command by leaving a suitably named file in a directory where you will run `-execdir`. Similarly, entries in PATH **should not be empty** or **non-absolute directory names**. If any invocation of the `+` form returns a non-zero exit status, find will also return a non-zero exit status. If find encounters an error, it may exit immediately, **meaning some pending commands might not run at all**. The result of the action depends on whether the `;` or `+` variant is used. `-execdir command {} +` always returns true, while `-execdir command {} ;` returns true only if the command returns 0.

#### -fls Create a file and write the result to it

##### Parameters
`file`

##### Description
This option always returns true. `-fls` is similar to `-ls` and `-fprint`, but it writes the results to a file. The output file is always created even if the predicate never matches. For information on how special characters in filenames are handled, see the "UNUSUAL FILENAMES" section in the man page.

#### -fprint Print full filename to a specified file

##### Parameters
`file`

##### Description
This option always returns true. If `file` does not exist when find is run, it is created; if it already exists, its content is truncated. Filenames `/dev/stdout` and `/dev/stderr` are handled specially and refer to standard output and standard error, respectively. The output file is always created even if the predicate never matches.

#### -fprint0

##### Parameters
`file`

##### Description
This option always returns true. Similar to `-print0`, but writes the output to a file; similar to `-fprint`. The output file is always created even if the predicate never matches.

#### -fprintf

##### Parameters
`file`

##### Description
This option always returns true. Similar to `-printf`, but writes the output to a file; similar to `-fprint`. The output file is always created even if the predicate never matches.

#### -ls List current file to standard output

##### *No Parameters*

##### Description
This option always returns true. List the current file in `ls -dils` format on standard output. The block counts are in 1 KB blocks unless the POSIXLY_CORRECT environment variable is set, in which case 512-byte blocks are used.

#### -ok Prompt the user before executing a command

##### Parameters
`command ;`

##### Description
Similar to `-exec`, but prompts the user first. If the user agrees, the command is run; otherwise, it returns false. If the command is run, its standard input is redirected from `/dev/null`. Responses to the prompt are matched against a pair of regular expressions to determine if they are affirmative or negative. If the POSIXLY_CORRECT environment variable is set, these regular expressions are obtained from the system; otherwise, they are obtained from find's message translations. If the system has no suitable definition, find's own definitions will be used. In either case, the interpretation of the regular expression itself is affected by the environment variables LC_CTYPE (character classes) and LC_COLLATE (character ranges and equivalence classes).

##### Related Options
- **-files0-from**: Cannot be specified simultaneously with `-ok`.

#### -okdir

##### Parameters
`command ;`

##### Description
Similar to `-execdir`, but prompts the user in the same manner as `-ok` before execution. If the user does not agree, it returns false. If the command is executed, its standard input is redirected from `/dev/null`.

##### Related Options
- **-files0-from**: Cannot be specified simultaneously with `-okdir`.

#### -print Print the full file name, followed by a newline

##### *No Parameters*

##### Description
This option always returns true. If you are piping the output of find into another program and the files you are searching for might contain newlines, you should consider using `-print0` instead of `-print`.

#### -print0 Print the full file name, followed by a null character

##### *No Parameters*

##### Description
This option always returns true. This allows filenames that contain newlines or other types of whitespace to be correctly interpreted by programs that process the find output. This option corresponds to the `-0` option of `xargs`.

#### -printf Format output

##### Parameters
`format`

Available escape characters and directives include:
- \a Alarm.
- \b Backspace.
- \c Stop printing immediately and flush output.
- \f Form feed.
- \n Newline.
- \r Carriage return.
- \t Horizontal tab.
- \v Vertical tab.
- \0 Null character.
- \\\ A literal backslash `\`.
- \NNN The character whose ASCII code is NNN (octal).
- A backslash character `\` followed by any other character is treated as an ordinary character, so both are printed.
- %% A literal percent sign.
- %a File's last access time in the format returned by the C ctime(3) function.
 ..... (More directives available in the man page)

##### Description
*Not available*

#### -prune If the file is a directory, do not descend into it

##### *No Parameters*

##### Description
This option always returns true.

##### Related Options
- **-depth**: If `-depth` is specified, `-prune` will have no effect.
- **-delete**: Because `-delete` implies `-depth`, you cannot effectively use both.

#### -quit Exit immediately

##### *No Parameters*

##### Description
Returns zero if no errors have occurred. This is different from `-prune`, as `-prune` only applies to the contents of pruned directories, while `-quit` causes find to stop immediately. No child processes will continue to run. Any command lines built by `-exec ... +` or `-execdir ... +` are invoked before the program exits. After `-quit` is executed, files specified on the command line will no longer be processed. For example, `find /tmp/foo /tmp/bar -print -quit` will only print `/tmp/foo`. A common use of `-quit` is to stop searching the filesystem once you have found what you are looking for.

### Global Options
Always return true. Global options also affect tests that appear earlier in the command line. To avoid confusion, global options should be specified **after the starting points and before the first test, positional option, or action**. If global options are specified elsewhere, find will issue a warning message explaining that this may be confusing.

> Global options appear after the list of starting points and are therefore not in the same category as options like `-L`.

#### -d Synonym for `-depth`

##### *No Parameters*

##### Description
Used for compatibility with FreeBSD, NetBSD, MacOS X, and OpenBSD.

#### -depth Process directory contents before the directory itself

##### Parameters
`levels`

##### Description
Process the contents of each directory before the directory itself. The `-delete` action also implies `-depth`.

#### -files0-from Read starting points from a file instead of the command line

##### Parameters
`file`

##### Description
Use this option to safely pass an arbitrary number of starting points to the find command. Using this option is **mutually exclusive** with passing starting points on the command line. The file parameter is mandatory. Starting points in the file must be separated by ASCII NUL characters. Two consecutive NUL characters (i.e., a starting point with a zero-length filename) are not allowed and will result in an error diagnostic and a non-zero exit code.

Unlike standard calls where find defaults to the current directory if no path is passed, this option requires the file to be present. Starting points are processed the same way as otherwise; for example, find will recursively enter subdirectories unless prevented. To process only the starting points, pass `-maxdepth 0`.

**Note**: If a file is listed multiple times in the input file, it is unspecified whether it will be visited multiple times. If the file is modified during the find operation, the result is also unspecified. Finally, the seek position in the named file when find exits (via `-quit` or otherwise) is also unspecified. **Unspecified** means it **may or may not work**, or **might not do anything specific**, and the behavior may vary across platforms or findutils versions.

> :bulb: You can use `-files0-from -` to **read the list of starting points from standard input**, for example from a pipe. In this case, `-ok` and `-okdir` actions are not allowed because they would interfere with reading from standard input for user confirmation.

> :warning: Warning: If the given file is empty, find will not process any starting points and will exit immediately after parsing the arguments.

#### -help, --help Print a summary of find command line usage and exit.

##### *No Parameters*

##### Description
*No description*

#### -ignore_readdir_race

##### *No Parameters*

##### Description
Normally, find will issue an error message when it cannot stat a file. If you **enable this option** and a file is **deleted between the time find reads the filename from the directory and the time it attempts to stat it**, no error message will be issued. This also applies to files or directories specified on the command line. This option takes effect when the command line is read, meaning you cannot enable it for one part of the filesystem and disable it for another (if you need to do this, you need to issue two find commands). Additionally, with `-ignore_readdir_race`, find will ignore errors from the `-delete` action if the file has disappeared after the parent directory was read: it will not output error diagnostics, and the return code of the `-delete` action will be true.

#### -maxdepth Maximum traversal level

##### Parameters
`levels`

##### Description
Descend at most `levels` (a non-negative integer) levels of directories below the starting points. `-maxdepth 0` means **apply the tests and actions only to the starting points themselves**.

#### -mindepth Minimum traversal level

##### Parameters
`levels`

##### Description
Do not apply any tests or actions at levels less than `levels` (a non-negative integer). `-mindepth 1` means **process all files except the starting points**.

#### -mount Do not descend directories on other filesystems

##### *No Parameters*

##### Description
This is an alternative name for `-xdev`, for compatibility with some other versions of find.

#### -noignore_readdir_race

##### *No Parameters*

##### Description
Turns off the effect of `-ignore_readdir_race`.

#### -noleaf Do not optimize by assuming directories contain 2 fewer subdirectories than their hard link count.

##### *No Parameters*

##### Description
Required when searching filesystems that do not follow Unix directory-link conventions, such as CD-ROMs, MS-DOS filesystems, or AFS volume mount points. On a normal Unix filesystem, each directory has at least 2 hard links: its name and its `.` entry. Additionally, its subdirectories (if any) each have a `..` entry pointing to that directory. When find examines a directory, after it has statted 2 fewer subdirectories than the directory's link count, it knows that the remaining entries in the directory are non-directories ("leaf" files in the directory tree). If only the files' names need to be examined, there is no need to stat them; this can significantly speed up the search.

#### -version, --version Print the find version number and exit.

##### *No Parameters*

##### Description
*No description*

#### -xdev Do not descend into directories on other filesystems.

##### *No Parameters*

##### Description
*No description*

### Positional Options
Always return true. They only affect subsequent tests in the command line.

#### -daystart Measure times from the beginning of today

> Used for `-amin`, `-atime`, `-cmin`, `-ctime`, `-mmin`, and `-mtime`.

##### *No Parameters*

##### Description
Measure times from the beginning of today rather than from 24 hours ago. This option only affects tests that appear later in the command line.

#### ~~-follow~~ Dereference symbolic links.

##### *No Parameters*

##### Description
**Deprecated; use the `-L` option instead.** Implies `-noleaf`. The `-follow` option only affects tests that appear after it in the command line. Unless the `-H` or `-L` option has been specified, the position of the `-follow` option changes the behavior of the `-newer` predicate; any files listed as arguments to `-newer` will be dereferenced if they are symbolic links. The same applies to `-newerXY`, `-anewer`, and `-cnewer`. Similarly, the `-type` predicate will always match against the type of the file a symbolic link points to rather than the link itself. Using `-follow` causes the `-lname` and `-ilname` predicates to always return false.

#### -regextype Change regular expression syntax

##### Parameters
`type`

##### Description
Changes the regular expression syntax understood by `-regex` and `-iregex` tests that appear later in the command line. To see known regular expression types, use `-regextype help`. The Texinfo documentation explains the meanings and differences between various regular expression types. If you do not use this option, find behaves as if `emacs` were specified.

#### -warn, -nowarn Turn warning messages on or off.

##### *No Parameters*

##### Description
These warnings apply only to command line usage, not to conditions find might encounter while searching directories. The default behavior is `-warn` if standard input is a `tty`, and `-nowarn` otherwise. If a warning message related to command line usage is produced, find's exit status is not affected. If the POSIXLY_CORRECT environment variable is set and `-warn` is also used, it is unspecified which (if any) warnings will be active.

### Operators
Operators are listed in order of decreasing precedence:
- `(expr)` Force precedence. Since parentheses have special meaning to the shell, they usually need to be quoted. Many examples use backslashes for this: `\(...\)` instead of `(...)`.
- `! expr` True if the expression is false (negation). This character also usually needs to be protected from shell interpretation.

> :bulb: Tip: When `-a` is specified implicitly (e.g., no explicit operator between two tests) or explicitly, it has higher precedence than `-o`. For example, `find . -name foo -o -name bar -print` will never print `foo`.

#### -not

##### Parameters
`expr`

##### Description
Equivalent to `! expr`, but not POSIX-compliant.

#### -a 

##### Parameters
`expr1` -a `expr2`

##### Description
Two consecutive expressions are treated as implicitly connected by `-a`; if `expr1` is false, `expr2` is not evaluated. Equivalent to `expr1 expr2`.

#### -and

##### Parameters
`expr1` -and `expr2`

##### Description
Same as `-a`. Not POSIX-compliant.

#### -o

##### Parameters
`expr1` -o `expr2`

##### Description
Both `expr1` and `expr2` are always evaluated. The value of `expr1` is discarded; the value of the list is the value of `expr2`. The comma operator (`,`) is useful for searching for several different types of things but only traversing the filesystem hierarchy once. The `-fprintf` action can be used to list various matches into several different output files. If `expr1` is true, `expr2` is not evaluated.

#### -or

##### Parameters
`expr1` -or `expr2`

##### Description
Same as `-o`. Not POSIX-compliant.

## Examples

Search all files in the current directory whose content contains "140.206.111.111":
```shell
find . -type f -name "*" | xargs grep "140.206.111.111"
```

#### Match by Filename or Regular Expression

List all files and folders in the current directory and its subdirectories:

```shell
find .
```

Find files ending in `.txt` in the `/home` directory:

```shell
find /home -name "*.txt"
```

Same as above, but case-insensitive:

```shell
find /home -iname "*.txt"
```

Find all files ending in `.txt` and `.pdf` in the current directory and subdirectories:

```shell
find . \( -name "*.txt" -o -name "*.pdf" \)

# OR

find . -name "*.txt" -o -name "*.pdf"
```

Match by file path or name:

```shell
find /usr/ -path "*local*"
```

Match file path based on regular expressions:

```shell
find . -regex ".*\(\.txt\|\.pdf\)$"
```

Same as above, but case-insensitive:

```shell
find . -iregex ".*\(\.txt\|\.pdf\)$"
```

#### Negation

Find files in `/home` that do not end in `.txt`:

```shell
find /home ! -name "*.txt"
```

#### Search by File Type

```shell
find . -type <type_parameter>
```

Type parameter list:

*    **f**  Regular file
*    **l**  Symbolic link
*    **d**  Directory
*    **c**  Character device
*    **b**  Block device
*    **s**  Socket
*    **p**  FIFO

#### Search Based on Directory Depth

Limit maximum depth to 3:

```shell
find . -maxdepth 3 -type f
```

Search for files at least 2 levels deep from the current directory:

```shell
find . -mindepth 2 -type f
```

#### Search Based on File Timestamps

```shell
find . -type f <timestamp_option>
```

Each file in a UNIX/Linux filesystem has three timestamps:

*    **Access time** (-atime/days, -amin/minutes): The last time the file was accessed.
*    **Modification time** (-mtime/days, -mmin/minutes): The last time the file's content was modified.
*    **Change time** (-ctime/days, -cmin/minutes): The last time the file's metadata (e.g., permissions) was changed.

Search for all files accessed in the last 7 days:

```shell
find . -type f -atime -7
```

Search for all files accessed exactly 7 days ago:

```shell
find . -type f -atime 7
```

Search for all files accessed more than 7 days ago:

```shell
find . -type f -atime +7
```

Search for all files accessed more than 10 minutes ago:

```shell
find . -type f -amin +10
```

Find all files modified more recently than `file.log`:

```shell
find . -type f -newer file.log
```

#### Match Based on File Size

```shell
find . -type f -size <size_unit>
```

File size units:

*    **b**  —— Blocks (512 bytes)
*    **c**  —— Bytes
*    **w**  —— Words (2 bytes)
*    **k**  —— Kilobytes
*    **M**  —— Megabytes
*    **G**  —— Gigabytes

Search for files larger than 10 KB:

```shell
find . -type f -size +10k
```

Search for files smaller than 10 KB:

```shell
find . -type f -size -10k
```

Search for files exactly 10 KB in size:

```shell
find . -type f -size 10k
```

#### Delete Matching Files

Delete all `.txt` files in the current directory:

```shell
find . -type f -name "*.txt" -delete
```

#### Match Based on File Permissions/Ownership

Search for files with 777 permissions in the current directory:

```shell
find . -type f -perm 777
```

Find `.php` files in the current directory that do not have 644 permissions:

```shell
find . -type f -name "*.php" ! -perm 644
```

Find all files owned by user `tom` in the current directory:

```shell
find . -type f -user tom
```

Find all files belonging to group `sunk` in the current directory:

```shell
find . -type f -group sunk
```

#### Using `-exec` with Other Commands

Find all files owned by `root` in the current directory and change ownership to `tom`:

```shell
find . -type f -user root -exec chown tom {} \;
```

In the example above, **{}** is used with the **-exec** option to match each file, which is then replaced by the corresponding filename.

Find all `.txt` files in your home directory and delete them:

```shell
find $HOME/. -name "*.txt" -ok rm {} \;
```

In the example above, **-ok** behaves like **-exec** but prompts the user for confirmation before performing the action.

Find all `.txt` files in the current directory and concatenate them into `all.txt`:

```shell
find . -type f -name "*.txt" -exec cat {} \; > /all.txt
```

Move `.log` files older than 30 days to the `old` directory:

```shell
find . -type f -mtime +30 -name "*.log" -exec cp {} old \;
```

Find all `.txt` files in the current directory and print them in the format "File: filename":

```shell
find . -type f -name "*.txt" -exec printf "File: %s\n" {} \;
```

Since multiple commands cannot be used directly within a single `-exec` parameter, you can invoke a script:

```shell
-exec ./test.sh {} \;
```

#### Search while Skipping Specified Directories

Find all `.txt` files in the current directory or subdirectories, but skip the `sk` subdirectory:

```shell
find . -path "./sk" -prune -o -name "*.txt" -print
```

> :warning: `./sk` cannot be written as `./sk/`, otherwise it will not work.

Ignore two directories:

```shell
find . \( -path ./sk -o -path ./st \) -prune -o -name "*.txt" -print
```

> :warning: If using relative paths, you must prepend them with `./`.

#### Other find Tips

List all files with zero length:

```shell
find . -empty
```

#### Other Examples

```shell
find ~ -name '*jpg' # Find all jpg files in the home directory. The -name parameter allows you to limit results to files matching a given pattern.
find ~ -iname '*jpg' # -iname is like -name, but case-insensitive.
find ~ \( -iname 'jpeg' -o -iname 'jpg' \) # Some images might have .jpeg extensions. We can combine patterns with OR (-o).
find ~ \( -iname '*jpeg' -o -iname '*jpg' \) -type f # Use -type f to ensure you are finding only files, in case there are directories ending in jpg.
find ~ \( -iname '*jpeg' -o -iname '*jpg' \) -type d # Find directories with these names instead.
```

Filter for files modified in the last week:

```shell
find ~ \( -iname '*jpeg' -o -iname '*jpg' \) -type f -mtime -7
```

You can filter by status change time (`ctime`), modification time (`mtime`), or access time (`atime`). These are in days; for finer control, use minutes (`cmin`, `mmin`, and `amin`). Use `+` (greater than) or `-` (less than) before the number unless you want an exact match.

Find large files (e.g., greater than 1 GB) in the `/var/log` directory:

```shell
find /var/log -size +1G
```

Find all files owned by `bcotton` in `/data`:

```shell
find /data -owner bcotton
```

Find files based on permissions. For example, find files in your home directory that are readable by everyone:

```shell
find ~ -perm -o=r
```

Delete automatically generated files under macOS:

```shell
find ./ -name '__MACOSX' -depth -exec rm -rf {} \;
```

Count lines of code, excluding empty lines:

```shell
find . -name "*.java" | xargs cat | grep -v ^$ | wc -l
```
