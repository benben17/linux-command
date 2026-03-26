fishshell
===

A smart and user-friendly shell, better than bash.

## Installation

```shell
# Ubuntu and Debian installation:
sudo apt-get install fish

# macOS installation:
brew install fish
```

## Startup and Help

Since `Fish` syntax differs significantly from `Bash`, `Bash` scripts are generally not compatible. It is recommended not to set `Fish` as your default shell immediately; instead, start it manually when needed.

```shell
# Start Fish after installation:
$ fish

# To get help while using Fish:
$ help
```

## Color Display

```shell
# Invalid commands are shown in red:
$ mkd

# Valid commands are shown in blue:
$ mkdir

# Valid paths are underlined. If there's no underline, the path does not exist:
$ cat ~/somefile
```

## Autosuggestions

Fish automatically provides suggestions behind the cursor in grey. To accept a suggestion, press `→` or `Control + F`. To accept only the first part of the suggestion, press `Alt + →`.

```shell
$ /bin/hostname      # Command suggestion
$ grep --ignore-case # Parameter suggestion
$ ls node_modules    # Path suggestion
```

## Auto-completion

When typing commands, `Fish` automatically shows matching entries from your history. If no history match is found, `Fish` guesses the possible results. For example, typing `pyt` and pressing `Tab` will autocomplete to the `python` command.

`Fish` also supports auto-completion for `Git` branches.

## Scripting Syntax

### if Statement

```shell
if grep fish /etc/shells
    echo Found fish
else if grep bash /etc/shells
    echo Found bash
else
    echo Got nothing
end
```

### switch Statement

```shell
switch (uname)
case Linux
    echo Hi Tux!
case Darwin
    echo Hi Hexley!
case FreeBSD NetBSD DragonFly
    echo Hi Beastie!
case '*'
    echo Hi, stranger!
end
```

### while Loop

```shell
while true
    echo "Loop forever"
end
```

### for Loop

```shell
for file in *.txt
    cp $file $file.bak
end
```

### Functions

Functions in `Fish` are used to encapsulate commands or create aliases.

```shell
function ll
    ls -lhG $argv
end
```

The code above defines an `ll` function. Once defined, you can use `ll` instead of `ls -lhG`. The `$argv` variable represents the function's arguments.

```shell
function ls
    command ls -hG $argv
end
```

The code above redefines the `ls` command. Note the use of `command` before `ls` inside the function body to prevent an infinite loop.

### Prompt

The `fish_prompt` function is used to define the command-line prompt.

```shell
function fish_prompt
  set_color purple
  date "+%m/%d/%y"
  set_color FF0
  echo (pwd) '>'
  set_color normal
end
```

After executing the function above, your prompt will look like this:

```
02/06/13
/home/tutorial > 
```

## Configuration

Fish's configuration file is located at `~/.config/fish/config.fish`. It is automatically loaded whenever `Fish` starts. Fish also provides a web-based interface for configuration.

```shell
$ fish_config # Opens the web interface in a browser
```

### Key Features Comparison:

- **Running Commands**: Compatible with bash-like execution.
- **Getting Help**: `help/man cmd` opens in browser/terminal.
- **Syntax Highlighting**: Real-time command validation.
- **Wildcards**: Supports recursive matching with `**`.
- **Pipes and Redirections**: Use `^` for stderr.
- **Autosuggestions**: Use `Ctrl-f` or `→` to autocomplete.
- **Tab Completions**: Powerful tab-based completion.
- **Variables**: Set using `set` (instead of `name=value`).
- **Exit Status**: Use `$status` instead of `$?`.
- **Exports**: Use `set -x` instead of `export`.
- **Lists**: All variables in Fish are actually lists.
- **Command Substitutions**: Use `(cmd)` instead of backticks or `$()`.
- **Combiners (And, Or, Not)**: Use words instead of symbols like `&&` or `||`.
- **Functions**: Use `$argv` instead of `$1`, `$2`, etc.
- **Conditionals/Loops**: Clean, Python-like syntax.
- **Startup**: Configured via `~/.config/fish/config.fish`.
- **Universal Variables**: Variables shared across all running Fish instances.

### Examples:

```shell
set name 'czl' # Set a variable
echo $name
echo $status   # Display exit status
env            # List environment variables
set -x MyVar Value # Export a variable
set -e MyVar       # Erase a variable
set PATH $PATH /usr/local/bin # Add to PATH list
set -U fish_user_paths /usr/local/bin $fish_user_paths # Permanent PATH update
touch "testing_"(date +%s)".txt" # Command substitution
cp file.txt file.txt.bak; and echo 'success'; or echo 'fail' # Combiners
functions # List defined functions
```

## References

- [Official Fish Shell Website](http://fishshell.com)
