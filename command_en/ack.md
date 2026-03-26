ack
===

A text search tool that is better than grep.


## Installation

```shell
# On Ubuntu, install ack-grep, as the name 'ack' is taken by other software in Debian-based systems.
sudo apt-get install ack-grep

# On Alpine Linux using the apk package manager:
apk add ack
```


## Options

These parameters are highly used in Linux, especially if you use Vim as an IDE.

```shell
-c (count) / -i (ignore case) / -h (no filename) /
-l (filenames only) / -n (line number) / -v (invert match)
```


## Features

The official ack website lists five main selling points for this tool:

1. **Very fast**: It only searches what's meaningful.
2. **User-friendly search**: It ignores things that are not your source code.
3. **Designed for source code search**: Accomplish tasks with fewer keystrokes.
4. **Highly portable**: Very lightweight and easy to port.
5. **Free and Open Source**.


## Examples

The usage can be roughly categorized into:

> Searching  
> Search output  
> File presentation  
> File finding  
> File inclusion/exclusion  

Common grep operations:

```shell
grep -r 'hello_world' # Simple recursive search
grep '^hello_world' . # Simple regex
ls -l | grep .py      # Pipe usage
```

### Searching

Simple text search, recursive by default.

```shell
ack-grep hello
ack-grep -i hello
ack-grep -v hello
ack-grep -w hello
ack-grep -Q 'hello*'
```

### Search Output

Processing search results, such as showing only filenames.

```shell
ack-grep --line=1       # Output the first line of all files
ack-grep -l 'hello'     # Filenames that contain the match
ack-grep -L 'print'     # Filenames that do NOT contain the match
```

### File Presentation

How the output is displayed. You can practice with these parameters:

```shell
ack-grep hello --pager='less -R'    # Display using less
ack-grep hello --noheading          # Do not show filename headers
ack-grep hello --nocolor            # Do not color match strings
```

### File Finding

Yes, it can find files, saving you the trouble of combining `find` and `grep`, even though the Linux philosophy is "one tool for one task."

```shell
ack-grep -f hello.py                # Find files matching the exact name
ack-grep -g hello.py$               # Find files matching a regex
ack-grep -g hello --sort-files      # Find and then sort results
```

### File Inclusion/Exclusion

File filtering is a very useful feature. If you've ever accidentally hit a keyword in a log file while searching project source code, you'll find this helpful.

```shell
ack-grep --python hello             # Search only in Python files
ack-grep -G hello.py$ hello         # Search only in files matching the regex
```

## References

- [Official ack Website](https://beyondgrep.com/)
