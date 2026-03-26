alias
===

Define or display aliases.


## Synopsis

```shell
alias [-p] [name[=value] ...]
```


## Main Purpose

- Simplify long commands.
- Define, modify, or display one or more aliases.


## Options

```shell
-p: Display all defined aliases.
name (optional): Specify the alias to define, modify, or display.
value (optional): The value of the alias.
```

### Return Value

`alias` returns true unless an alias you try to display is undefined.


## Examples

```shell
# Display all defined aliases
alias
alias -p

# Display specific defined aliases (assuming they exist in the current environment)
alias ls
alias ls grep

# Define or modify an alias
alias ls='ls --color=auto'
alias ls='ls --color=never' grep='grep --color=never'
```


## Knowledge Points

Aliases set directly in the shell will be lost after the terminal is closed or the system is restarted. How can they be made permanent?

Open `~/.bashrc` with an editor and add your alias settings, for example: `alias rm='rm -i'`. After saving, execute `source ~/.bashrc` to apply the changes. This will permanently save the command aliases.

Since this modifies the `~/.bashrc` file in the current user's directory, it only affects the current user. To make it effective for all users, modify the `/etc/bashrc` file instead.

> Note: The following may vary depending on your system:
>
> On CentOS 7, this file is `/etc/bash.bashrc`. Additionally, if you examine `~/.bashrc` on CentOS 7, you might find a block of code like this:
>
> ```shell
> if [ -f ~/.bash_aliases ]; then
>   . ~/.bash_aliases
> fi
> ```
>
> This code means that if `.bash_aliases` exists, it will be loaded. You can create this file in your home directory to store your alias settings separately.


## Incorrect Usage

- The alias to be displayed is undefined.
- When defining or modifying an alias, failing to wrap the value in **single quotes** if it contains spaces can lead to serious issues:

```shell
# Clear all aliases for demonstration
unalias -a
# Not wrapped in single quotes
alias rm=rm -rf
# Execution results in an error: bash: alias: -rf: not found
# Checking with 'alias' returns: alias rm='rm'
```

```shell
# A more confusing example
# Clear all aliases for demonstration
unalias -a
# Still not wrapped in single quotes
alias ls=ls --color=never
# Execution appears to succeed without error

# Checking with 'alias' reveals:
# alias --color=never
# alias ls='ls'
# The 'alias' command treated these as two separate groups.
```


## Q&A

Q: What happens if I try to display multiple aliases and some are undefined?

A: Run it as usual; `alias` will continue to process the remaining arguments even if one is undefined.

Q: What if I define `alias cd='ls' ls='cd'`?

A: Running `cd` will still change the directory, and `ls` will still list files. Do not define aliases this way.


### Notes

1. When executing scripts:
    - If a bash script executed with the `source` command runs `alias` or `unalias`, it may affect the terminal environment's alias settings; conversely, terminal aliases can affect the script's results.
    - Bash scripts called via `sh` or executed directly (with execution permissions) are not affected by terminal environment aliases.
2. To remove an alias, see the `unalias` command.
3. It is recommended NOT to use dangerous options like `-f` in aliases for commands like `mv`, `cp`, or `rm` (e.g., `alias rm='rm -f'`).
4. Be aware of potential conflicts between aliases and other commands.
5. This is a bash built-in command; for more help, use the `help` command.

### Other References

- [alias(1p) - Linux manual page](https://man7.org/linux/man-pages/man1/alias.1p.html)
