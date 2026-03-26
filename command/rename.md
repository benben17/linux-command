rename
===

Batch changes filenames using string replacement.

## Description

There are two versions of the `rename` command, and their usage differs.

```bash
C language version, supports wildcards
[Common wildcards]
?    Represents any single character
*    Represents any single character or string of characters

Perl version, supports regular expressions
[Common regular expression symbols]
^    Matches the start of the input
$    Matches the end of the input
.    Matches any single character except a newline
+    Matches the preceding character one or more times. For example, "zo+" matches "zoo", but not "z"
[a-z]    Represents a range of characters. For example, "[a-z]" matches any lowercase letter between "a" and "z".
[^m-z]   Negated character range. Matches characters not in the specified range.
```

Distinction method: `rename --version`

If the returned result contains **util-linux**, it is the C language version; otherwise, it is the Perl version.
```bash
# Perl version | Ubuntu (18), Mint (20) use the Perl version by default
$ rename --version
/usr/bin/rename using File::Rename version 1.10

# C language version | CentOS (7) uses the C language version by default
$ rename --version
rename from util-linux 2.23.2
```

### Syntax

```bash
# Perl version
rename [ -h|-m|-V ] [ -v ] [ -0 ] [ -n ] [ -f ] [ -d ] [ -e|-E perlexpr]*|perlexpr [ files ]

# C language version
rename [options] expression replacement file...
```

### Parameters

```bash
# Perl version
-v, --verbose
        Detailed: Print names of successfully renamed files.

-0, --null
        Use \0 as the record separator when reading from STDIN.

-n, --nono
        No action: Print filenames to be renamed, but do not rename them.

-f, --force
        Overwrite: Allow overwriting existing files.

--path, --fullpath
        Rename full path: Include any directory components. Default.

-d, --filename, --nopath, --nofullpath
        Do not rename directory: Rename only the filename part of the path.

-h, --help
        Help: Print synopsis and options.

-m, --man
        Manual: Print the manual page.

-V, --version
        Version: Display version number.

-e      Expression: Code acting on filenames.
        Can be repeated to build up the code (like "perl -e"). Without -e, the first argument is used as the code.

-E      Statement: Code acting on filenames, like -e, but terminated by ';'.

# C language version
-v, --verbose
        Provide visual feedback on which files (if any) are renamed.

-V, --version
        Display version information and exit.

-s, --symlink
        Perform rename on symbolic link targets.

-h, --help
        Display help text and exit.
```

### Examples

---

#### Perl Version

Rename `1.txt` and `2.txt` to `1.log` and `2.log`:

```bash
$ rename -v "s/txt/log/g" 1.txt 2.txt
1.txt renamed as 1.log
2.txt renamed as 2.log
```

Change file extension:

```bash
rename "s//.html//.php/" *     # Change .html extension to .php extension
```

Batch add file extension:

```bash
rename "s/$//.txt/" *  # Append .txt to all filenames
```

Batch remove file extension:

```bash
rename "s//.txt//" *   # Remove .txt extension from all filenames ending in .txt
```

---

##### C Language Version

Rename `1.txt` and `2.txt` to `1.log` and `2.log`:

```bash
$ rename -v txt log 1.txt 2.txt
`1.txt' -> `1.log'
`2.txt' -> `2.log'
```

If a folder contains files `foo1, ..., foo9, foo10, ..., foo278`:
```bash
# Rename foo1 to foo9 as foo01 to foo09; only renames files with 4-character names, replacing "foo" with "foo0".
rename foo foo0 foo?

# Rename all files from foo01 to foo99 as foo001 to foo099; only renames files with 5-character names, replacing "foo" with "foo0".
rename foo foo0 foo??

# Rename all files from foo001 to foo278 as foo0001 to foo0278; all files starting with "foo" are renamed.
rename foo foo0 foo*

# Rename all files from foo0200 to foo0278 as foo200 to foo278; "foo0" in the filename is replaced with "foo".
rename foo0 foo foo0[2]*
```
