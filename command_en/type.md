type
===

Display information about command type.

## Synopsis

```shell
 type [-afptP] name [name ...]
 ```

## Main Purpose

- Display information about the searched command.
- Control search scope and behavior.
- Display the highest-priority type for the searched command.

## Options

```shell
-a: Search the PATH environment variable and display all executable file paths containing 'name'. If '-p' is not given, also display information if 'name' exists as an alias, keyword, function, or built-in.
-f: Exclude shell functions from the search.
-p: Returns nothing if 'type -t name' would not return 'file'. Otherwise, search the PATH and return the executable file path.
-P: Even if 'name' is an alias, built-in, or function, search the PATH and return the executable file path.
-t: Returns a single word describing the type of 'name' (alias, keyword, function, builtin, file). Returns empty if not found.
```

## Parameters

name: The command(s) to search for.

## Return Value

Returns success if the specified command(s) can be found, otherwise returns failure.

## Examples

```shell
The following examples assume '~/.bashrc' defines the following:

alias ls='ls --color=auto'
mybash(){ vim ~/.bashrc; }

And built-in commands are not disabled using 'enable'.
```

```shell
type -a mybash
# Output
mybash is a function
mybash ()
{
    vim ~/.bashrc
}

type -a -f mybash
# Output (error because functions are excluded)
bash: type: mybash: not found

type -a -p mybash
# Output is empty (nothing returned because functions are excluded)

type -a ls
# Output
ls is aliased to `ls --color=auto'
ls is /usr/bin/ls
ls is /bin/ls

type -a -p ls
# Output
/usr/bin/ls
/bin/ls
```

```shell
# '-f' does not affect the scope of '-P'; using '-f' with '-p' is not recommended.
# Note: printf is both a built-in command and an executable (GNU coreutils); built-in takes priority.

type -p printf
# Output is empty

type -P printf
# Output
/usr/bin/printf
/bin/printf
```

```shell
# If multiple types exist, the one with the highest priority is output.

type -t ls
# Output
alias

type -t for
# Output (bash keyword)
keyword

type -t mybash
# Output
function

type -t -f mybash
# Output empty

type -t printf
# Output (bash built-in has higher priority)
builtin

type -t chmod
# Output
file
```

### Notes

1. This command is a bash built-in; see the `help` command for related help information.
2. For command priority issues, see the `builtin` command.
