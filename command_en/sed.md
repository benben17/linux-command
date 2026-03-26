sed
===

A powerful stream-oriented text editor.

## Description

**sed** is a stream editor and a crucial tool in text processing, working perfectly with regular expressions. During processing, it stores the current line being handled in a temporary buffer called the "pattern space," then processes the buffer's content with `sed` commands and sends the result to the screen. It then moves to the next line, repeating this until the end of the file. The file content itself does not change unless you use redirection to save the output. `sed` is primarily used for automatically editing one or more files, simplifying repetitive operations on files, and writing conversion programs.

## Options, Commands, and Replacement Flags

**Command Format**

```shell
sed [options] 'command' file(s)
sed [options] -f scriptfile file(s)
```

### Options

```shell
-e<script> or --expression=<script>: Process the input text file using the specified script.
-f<scriptfile> or --file=<scriptfile>: Process the input text file using the script file.
-h or --help: Display help.
-n, --quiet, --silent: Only display the result of script processing.
-V or --version: Display version information.
```

### Parameters

File: Specifies the list of text files to be processed.

### sed Commands

```shell
a\ # Insert text below the current line.
i\ # Insert text above the current line.
c\ # Change the selected lines to new text.
d # Delete the selected lines.
D # Delete the first line of the pattern space.
s # Substitute specified characters.
h # Copy the pattern space content to the hold buffer.
H # Append the pattern space content to the hold buffer.
g # Get the hold buffer content and replace the current pattern space text.
G # Get the hold buffer content and append it after the current pattern space text.
l # List non-printable characters.
n # Read the next input line and process it with the next command instead of the first.
N # Append the next input line to the pattern space with an embedded newline, changing the current line number.
p # Print the lines in the pattern space.
P # (Uppercase) Print the first line of the pattern space.
q # Quit sed.
b label # Branch to a labeled spot in the script; if the label doesn't exist, branch to the end of the script.
r file # Read lines from 'file'.
t label # Conditional branch; if the last 's' command succeeded, branch to the label.
T label # Error branch; if the last 's' command failed, branch to the label.
w file # Write and append the pattern space to 'file'.
W file # Write and append the first line of the pattern space to 'file'.
! # Apply the following command to lines not selected.
= # Print the current line number.
# # Comment extending to the next newline.
```

### sed Replacement Flags

```shell
g # Global substitution within a line.
p # Print the line.
w # Write the line to a file.
x # Swap the contents of the pattern space and the hold buffer.
y # Translate one character to another (not used with regular expressions).
\1 # Substring match flag.
& # Matched string flag.
```

### sed Metacharacters

```shell
^ # Match the beginning of a line. E.g., /^sed/ matches all lines starting with 'sed'.
$ # Match the end of a line. E.g., /sed$/ matches all lines ending with 'sed'.
. # Match any single non-newline character. E.g., /s.d/ matches 's' followed by any character and then 'd'.
* # Match zero or more occurrences of the preceding character.
[] # Match any character within the range. E.g., /[sS]ed/ matches 'sed' or 'Sed'.
[^] # Match any character not in the range.
\(..\) # Match a substring and save it. E.g., s/\(love\)able/\1rs/ replaces 'loveable' with 'lovers'.
& # Save the searched character for replacement. E.g., s/love/**&**/ results in **love**.
\< # Match the beginning of a word.
\> # Match the end of a word.
x\{m\} # Repeat character 'x' exactly m times.
x\{m,\} # Repeat character 'x' at least m times.
x\{m,n\} # Repeat character 'x' between m and n times.
```

## sed Usage Examples

### Substitution: s command

Replace a string in a file:

```shell
sed 's/book/books/' file
```

The **-n option** and **p command** used together print only the lines where substitution occurred:

```shell
sed -n 's/test/TEST/p' file
```

Use the **-i option** to edit the file directly, replacing all occurrences of 'book' with 'books':

```shell
sed -i 's/book/books/g' file
```

### Global Substitution Flag: g

The `/g` suffix replaces all matches in each line:

```shell
sed 's/book/books/g' file
```

To start substitution from the Nth match, use `/Ng`:

```shell
echo sksksksksksk | sed 's/sk/SK/2g'
skSKSKSKSKSK

echo sksksksksksk | sed 's/sk/SK/3g'
skskSKSKSKSK
```

### Delimiters

The `/` character is used as a delimiter in the above commands, but any character can be used:

```shell
sed 's:test:TEXT:g'
sed 's|test|TEXT|g'
```

If the delimiter appears within the pattern, it must be escaped:

```shell
sed 's/\/bin/\/usr\/local\/bin/g'
```

### Deletion: d command

Delete blank lines:

```shell
sed '/^$/d' file
```

Delete the 2nd line:

```shell
sed '2d' file
```

Delete from the 2nd line to the end:

```shell
sed '2,$d' file
```

Delete the last line:

```shell
sed '$d' file
```

Delete lines starting with 'test':

```shell
sed '/^test/d' file
```

### Matched String Flag: &

The regex `\w\+` matches every word; replace it with `[&]`, where `&` represents the matched word:

```shell
echo this is a test line | sed 's/\w\+/[&]/g'
[this] [is] [a] [test] [line]
```

Replace lines starting with '192.168.0.1' with itself plus 'localhost':

```shell
sed 's/^192.168.0.1/&localhost/' file
```

### Substring Match Flag: \1

Match a part of a given pattern:

```shell
echo this is digit 7 in a number | sed 's/digit \([0-9]\)/\1/'
this is 7 in a number
```

`digit 7` is replaced by `7`. The matched substring is `7`, captured by `\(..\)` and referenced by `\1`.

```shell
echo aaa BBB | sed 's/\([a-z]\+\) \([A-Z]\+\)/\2 \1/'
BBB aaa
```

### Case Conversion: \U, \L

```shell
\u: Convert the first letter to uppercase.
\U: Convert everything to uppercase.
\l: Convert the first letter to lowercase.
\L: Convert everything to lowercase.
```

Convert the first letter to uppercase:

```shell
sed 's/^[a-z]\+/\u&/' passwd
```

Convert matched characters to uppercase:

```shell
sed 's/^[a-z]\+/\U&/' passwd
```

### Combining Multiple Expressions

1. Replace multiple strings:

```shell
sed -e 's/old/new/g' -e 's/another_old/another_new/g' file.txt
```

2. Delete multiple lines:

```shell
sed -e '1d' -e '/pattern/d' file.txt
```

### Referencing Variables

Use double quotes if the expression contains variables:

```shell
test=hello
echo hello WORLD | sed "s/$test/HELLO/"
HELLO WORLD
```

### Selecting Line Ranges: , (Comma)

Print all lines within the range defined by patterns 'test' and 'check':

```shell
sed -n '/test/,/check/p' file
```

### Multi-point Editing: -e

```shell
sed -e '1,5d' -e 's/test/check/' file
```

### Reading from a File: r command

Read content from 'file' and display it after the line matching 'test':

```shell
sed '/test/r file' filename
```

### Writing to a File: w command

Write all lines containing 'test' in 'example' to 'file':

```shell
sed -n '/test/w file' example
```

### Appending (Below Line): a\ command

Append 'this is a test line' after lines starting with 'test':

```shell
sed '/^test/a\this is a test line' file
```

### Inserting (Above Line): i\ command

Insert 'this is a test line' before lines starting with 'test':

```shell
sed '/^test/i\this is a test line' file
```

### Changing Lines: c\ command

Replace lines starting with 'root' with new content:

```shell
sed '/^root/c\this is new line!' passwd
```

### Next: n command

If 'test' is matched, move to the next line and replace 'aa' with 'bb':

```shell
sed '/test/{ n; s/aa/bb/; }' file
```

### Transform: y command

Transform characters a-e to uppercase in lines 1-10:

```shell
sed '1,10y/abcde/ABCDE/' file
```

### Quit: q command

Quit sed after printing the first 10 lines:

```shell
sed '10q' file
```

### Hold and Get: h and G commands

```shell
sed -e '/test/h' -e '$G' file
```

Lines containing 'test' are copied to the hold buffer. At the last line, the G command appends the hold buffer content to the end of the file.

### Hold and Exchange: h and x commands

Swap the contents of the pattern space and the hold buffer:

```shell
sed -e '/test/h' -e '/check/x' file
```

### Script Files

```shell
sed [options] -f scriptfile file(s)
```

### Printing Odd or Even Lines

```shell
sed -n 'p;n' test.txt  # Odd lines
sed -n 'n;p' test.txt  # Even lines
```

### Printing the Line Following a Match

```shell
sed -n '/SCC/{n;p}' URFILE
```
