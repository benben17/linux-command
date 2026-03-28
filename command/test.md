test
===

Evaluate conditional expressions.

## Synopsis

```shell
test [expr]
# Or use square brackets (must have spaces inside):
[ EXPRESSION ]
```

## Main Purpose

- Evaluate conditional expressions and return boolean values (true/false)
- Commonly used with `if` statements for logical control in shell scripts
- Can perform three types of tests: numeric, string, and file tests

## File Test Operators

The `test` command is most commonly used to check file attributes:

| Operator | Description | Example |
|----------|-------------|---------|
| `-e FILE` | File exists | `[ -e file.txt ]` |
| `-f FILE` | Is a regular file | `[ -f /path/to/file ]` |
| `-d FILE` | Is a directory | `[ -d /path/to/dir ]` |
| `-r FILE` | Is readable | `[ -r file.txt ]` |
| `-w FILE` | Is writable | `[ -w file.txt ]` |
| `-x FILE` | Is executable | `[ -x script.sh ]` |
| `-s FILE` | File size > 0 | `[ -s logfile ]` |
| `-L FILE` | Is a symbolic link | `[ -L symlink ]` |
| `-a FILE` | True if file exists (same as -e) | `[ -a file.txt ]` |
| `-b FILE` | Is block special | `[ -b /dev/sda ]` |
| `-c FILE` | Is character special | `[ -c /dev/tty ]` |
| `-g FILE` | Is set-group-id | `[ -g file ]` |
| `-h FILE` | Is a symbolic link (same as -L) | `[ -h symlink ]` |
| `-k FILE` | Has sticky bit set | `[ -k file ]` |
| `-p FILE` | Is a named pipe | `[ -p pipe ]` |
| `-S FILE` | Is a socket | `[ -S socket ]` |
| `-t FD` | FD is opened on a terminal | `[ -t 0 ]` |
| `-u FILE` | Is set-user-id | `[ -u file ]` |
| `-O FILE` | Effectively owned by you | `[ -O file ]` |
| `-G FILE` | Effectively owned by your group | `[ -G file ]` |
| `-N FILE` | Modified since last read | `[ -N file ]` |
| `FILE1 -nt FILE2` | FILE1 is newer than FILE2 | `[ file1 -nt file2 ]` |
| `FILE1 -ot FILE2` | FILE1 is older than FILE2 | `[ file1 -ot file2 ]` |
| `FILE1 -ef FILE2` | FILE1 is a hard link to FILE2 | `[ file1 -ef file2 ]` |

### Example Script:

```shell
#!/bin/bash
file="/etc/passwd"
if [ -e "$file" ]; then
    echo "$file exists"
    if [ -r "$file" ]; then
        echo "and is readable"
    fi
else
    echo "$file does not exist"
fi
```

Output:
```
/etc/passwd exists
and is readable
```

## String Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `-z STRING` | String is empty | `[ -z "$var" ]` |
| `-n STRING` | String is not empty | `[ -n "$var" ]` |
| `STRING` | String is not empty | `[ "$var" ]` |
| `STRING1 = STRING2` | Strings are equal | `[ "$var1" = "$var2" ]` |
| `STRING1 != STRING2` | Strings are not equal | `[ "$var1" != "$var2" ]` |
| `STRING1 < STRING2` | STRING1 sorts before STRING2 | `[ "$a" < "$b" ]` |
| `STRING1 > STRING2` | STRING1 sorts after STRING2 | `[ "$a" > "$b" ]` |

**Important:** Always quote string variables to prevent syntax errors from empty variables.

### Example:

```shell
#!/bin/bash
read -p "Enter username: " username
if [ -z "$username" ]; then
    echo "Error: username cannot be empty"
    exit 1
elif [ "$username" = "root" ]; then
    echo "Warning: not recommended to use root account"
else
    echo "Welcome, $username"
fi
```

## Numeric Comparison Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `-eq` | Equal to | `[ "$a" -eq "$b" ]` |
| `-ne` | Not equal to | `[ "$a" -ne "$b" ]` |
| `-gt` | Greater than | `[ "$a" -gt "$b" ]` |
| `-ge` | Greater than or equal to | `[ "$a" -ge "$b" ]` |
| `-lt` | Less than | `[ "$a" -lt "$b" ]` |
| `-le` | Less than or equal to | `[ "$a" -le "$b" ]` |

### Example:

```shell
#!/bin/bash
read -p "Enter age: " age
if [ "$age" -lt 0 ]; then
    echo "Age cannot be negative"
elif [ "$age" -lt 18 ]; then
    echo "Minor"
elif [ "$age" -ge 18 ] && [ "$age" -lt 60 ]; then
    echo "Adult"
else
    echo "Senior"
fi
```

## Logical Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `! EXPR` | Logical NOT | `[ ! -f "$file" ]` |
| `EXPR1 -a EXPR2` | Logical AND | `[ "$a" -eq 1 -a "$b" -eq 2 ]` |
| `EXPR1 -o EXPR2` | Logical OR | `[ "$a" -eq 1 -o "$b" -eq 2 ]` |

**Modern recommended syntax:** Use `&&` and `||` instead of `-a` and `-o` for POSIX compliance:

```shell
[ "$a" -eq 1 ] && [ "$b" -eq 2 ]  # AND
[ "$a" -eq 1 ] || [ "$b" -eq 2 ]  # OR
```

## Other Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `-o OPTION` | Shell option is enabled | `[ -o nounset ]` |
| `-v VAR` | Shell variable is set | `[ -v myvar ]` |
| `-R VAR` | Shell variable is set and is a name reference | `[ -R myvar ]` |

## Advanced Syntax: [[ ]] and (( ))

Bash provides more powerful test syntax:

### Double brackets `[[ ]]`
- Pattern matching: `[[ "$var" == *.txt ]]`
- Regular expressions: `[[ "$var" =~ ^[0-9]+$ ]]`
- Safer string handling

### Double parentheses `(( ))`
- Designed for numeric comparisons: `(( a > b ))`
- Supports complex arithmetic expressions

```shell
if [[ "$file" == *.log ]]; then
    echo "This is a log file"
fi

if (( $count > 10 )); then
    echo "Count exceeds 10"
fi
```

## Return Value

Returns 0 if the expression evaluates to success, and returns 1 if the expression evaluates to failure or if invalid parameters are given.

## Practical Examples

### 1. Check if a service is running

```shell
#!/bin/bash
service="nginx"
if systemctl is-active --quiet "$service"; then
    echo "$service is running"
else
    echo "$service is not running"
    # Can add command to start the service here
fi
```

### 2. Backup file check

```shell
#!/bin/bash
backup_file="/backups/data_$(date +%Y%m%d).tar.gz"
if [ ! -f "$backup_file" ]; then
    echo "Error: backup file $backup_file does not exist"
    exit 1
elif [ ! -s "$backup_file" ]; then
    echo "Warning: backup file is empty"
else
    echo "Backup verification successful"
fi
```

### 3. Basic usage examples

```shell
# Execute a conditional expression and show the return value
[root@pc root]$ test ! "abc" == 123; echo $?
0

# Equivalent form using square brackets (note the spaces)
[root@pc root]$ [ ! "abc" == 123 ]; echo $?
0

# Using double brackets
[root@pc root]$ [[ ! "abc" == 123 ]]; echo $?
0
```

## Common Errors and Debugging Tips

### Common Mistakes:

1. **Missing spaces**: `[ "$a"="$b" ]` is incorrect, correct is `[ "$a" = "$b" ]`
2. **Unquoted variables**: `[ -f $file ]` should be `[ -f "$file" ]`
3. **Confusing string and numeric comparison**: Use `=` for strings, `-eq` for numbers

### Debugging Tips:

Add `set -x` at the beginning of the script to enable debug mode, or use `echo` to print test expressions:

```shell
echo "Test expression: [ $a -eq $b ]"
[ "$a" -eq "$b" ] && echo "True" || echo "False"
```

## Notes

1. This command is equivalent to `[`.
2. To write bash conditional expressions, you can use the built-in command `test`, `[`, or the compound command `[[`.
   - For conditional expressions, see [here](http://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html#Bash-Conditional-Expressions).
   - For an index of built-in commands, see [here](http://www.gnu.org/software/bash/manual/html_node/Builtin-Index.html#Builtin-Index).
   - For an index of compound commands, see [here](http://www.gnu.org/software/bash/manual/html_node/Reserved-Word-Index.html#Reserved-Word-Index).
3. This command is a bash built-in; see the `help` command for related help information.
