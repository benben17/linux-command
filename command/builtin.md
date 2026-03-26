builtin
===

Execute shell built-in commands.

## Synopsis

```shell
builtin [shell-builtin [arg ...]]
```

## Main Purpose

- Used to execute specified bash built-in commands.
- The bash built-in commands called by the `builtin` command take precedence over external commands or shell functions with the same name.

## Parameters

shell-builtin (optional): The bash built-in command to be called.

arg (optional): One or more arguments to be passed to the bash built-in command.

## Return Value

Returns the exit status of the built-in command, unless the argument is not a bash built-in command or the built-in command is disabled.

## Examples

Precedence order when names are identical:

`builtin` built-in > function > built-in > external command

```shell
# For cases where external commands have the highest precedence, please refer to the enable command.
# At this time, the built-in command is prioritized
echo "the Great Wall"
# Call the built-in command type, which returns the type of the command (builtin)
type -t echo
# Define an echo function
echo(){
    printf "123\n"
}
# At this time, the function with the same name is prioritized, displaying (123)
echo
# Call the built-in command type, which returns the type of the command (function)
type -t echo
# Now use the built-in command directly
builtin echo -e "backslash \\"
```

```shell
# Execute internal shell commands to output command aliases in the current system
builtin alias
alias cp='cp -i'
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

### Notes

1. This command is a bash built-in; for related help information, please use the `help` command.
2. If the built-in command to be called is disabled (including `builtin` itself), an error will occur. For information on disabling and enabling built-in commands, please refer to the `enable` command.
