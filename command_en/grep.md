grep
===

A powerful text search tool.

## Supplemental Information

**grep** (Global search Regular Expression and Print) is a powerful text search tool that searches for a specified pattern (using regular expressions) and prints the matching lines. It is highly flexible and commonly used to filter or search for specific characters in conjunction with various other commands.

### Options

```shell
-a, --text                 # Do not ignore binary data.
-A <num>, --after-context=<num> # Display <num> lines of trailing context after matching lines.
-b, --byte-offset          # Print the byte offset within the input file before each line of output.
-B <num>, --before-context=<num> # Display <num> lines of leading context before matching lines.
-c, --count                # Print a count of matching lines for each input file.
-C <num>, --context=<num>  # Display <num> lines of leading and trailing output context.
-d <action>, --directories=<action> # If an input file is a directory, use <action> (read, skip, or recurse).
-e <pattern>, --regexp=<pattern> # Use <pattern> as the search pattern.
-E, --extended-regexp      # Interpret pattern as an extended regular expression (ERE).
-f <file>, --file=<file>   # Obtain patterns from <file>, one per line.
-F, --fixed-strings        # Interpret pattern as a list of fixed strings.
-G, --basic-regexp         # Interpret pattern as a basic regular expression (BRE).
-h, --no-filename          # Suppress the prefixing of file names on output.
-H, --with-filename        # Print the file name for each match.
-i, --ignore-case          # Ignore case distinctions.
-l, --files-with-matches   # Print only names of files with matching lines.
-L, --files-without-match  # Print only names of files without matching lines.
-n, --line-number          # Prefix each line of output with its 1-based line number.
-P, --perl-regexp          # Interpret pattern as a Perl-compatible regular expression (PCRE).
-q, --quiet, --silent      # Quiet; do not write anything to standard output.
-R, -r, --recursive        # Read all files under each directory, recursively.
-s, --no-messages          # Suppress error messages about nonexistent or unreadable files.
-v, --revert-match         # Invert the sense of matching, to select non-matching lines.
-V, --version              # Display version information.
-w, --word-regexp          # Select only those lines containing matches that form whole words.
-x, --line-regexp          # Select only those matches that exactly match the whole line.
-y                         # Obsolete synonym for -i.
-o, --only-matching        # Show only the part of a matching line that matches the pattern.
-m <num>, --max-count=<num> # Stop reading a file after <num> matching lines.
```

### Regular Expressions

```shell
^    # Anchors the beginning of a line. e.g., '^grep' matches lines starting with grep.
$    # Anchors the end of a line. e.g., 'grep$' matches lines ending with grep.
.    # Matches any single character except newline.
*    # Matches zero or more occurrences of the preceding character.
.*   # Matches any string of characters.
[]   # Matches any single character in the brackets. e.g., '[Gg]rep' matches Grep and grep.
[^]  # Matches any single character NOT in the brackets.
\(..\) # Groups characters and marks them (capture group).
\<      # Anchors the beginning of a word.
\>      # Anchors the end of a word.
x\{m\}  # Matches character x exactly m times.
x\{m,\} # Matches character x at least m times.
x\{m,n\} # Matches character x at least m times but no more than n times.
\w    # Matches word characters (alphanumeric and underscore, [A-Za-z0-9_]).
\W    # Matches non-word characters.
\b    # Anchors at a word boundary.
```

## Common Usage of the grep Command

Search for a word in a file, returning lines containing **"match_pattern"**:

```shell
grep match_pattern file_name
grep "match_pattern" file_name
```

Search across multiple files:

```shell
grep "match_pattern" file_1 file_2 file_3 ...
```

Invert match (exclude lines) using the **-v** option:

```shell
grep -v "match_pattern" file_name
```

Colorize output using the **--color=auto** option:

```shell
grep "match_pattern" file_name --color=auto
```

Use extended regular expressions with the **-E** option:

```shell
grep -E "[1-9]+"
# or
egrep "[1-9]+"
```

Use Perl regular expressions with the **-P** option:

```shell
grep -P "(\d{3}\-){2}\d{4}" file_name
```

Output only the matching part of the line using the **-o** option:

```shell
echo this is a test line. | grep -o -E "[a-z]+\."
# Output: line.
```

Count the number of matching lines using the **-c** option:

```shell
grep -c "text" file_name
```

Search command history for `git` commands:

```shell
history | grep git
```

Display line numbers for matches using the **-n** option:

```shell
grep "text" -n file_name
```

Display the byte offset of the match:

```shell
echo gun is not unix | grep -b -o "not"
# Output: 7:not
```

List the names of files that contain the matching text:

```shell
grep -l "text" file1 file2 file3...
```

### Recursive Search with grep

Recursively search through directories:

```shell
grep "text" . -r -n
# '.' represents the current directory.
```

Ignore case sensitivity:

```shell
echo "hello world" | grep -i "HELLO"
# Output: hello world
```

Specify multiple matching patterns with the **-e** option:

```shell
echo this is a text line | grep -e "is" -e "line" -o
```

Include or exclude specific files during a recursive search:

```shell
# Search only in .php and .html files
grep "main()" . -r --include *.{php,html}

# Exclude all README files
grep "main()" . -r --exclude "README"

# Exclude files listed in 'filelist'
grep "main()" . -r --exclude-from filelist
```

Use null-byte terminator with xargs for filenames:

```shell
grep "aaa" file* -lZ | xargs -0 rm
```

Silent output (used for condition testing):

```shell
grep -q "test" filename
```

Print context around matching lines:

```shell
# Display 3 lines of trailing context after the match
seq 10 | grep "5" -A 3

# Display 3 lines of leading context before the match
seq 10 | grep "5" -B 3

# Display 3 lines of context around the match
seq 10 | grep "5" -C 3
```
