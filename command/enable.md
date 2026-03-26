enable
===

Enable or disable shell built-in commands.

### Synopsis

enable [-a] [-dnps] [-f filename] [name ...]

### Description

- Disable one or more built-in commands.
- Enable one or more built-in commands.
- Directly call an external command with the same name as a disabled built-in, found in the `$PATH`.
- Print all built-in commands, whether disabled or not.
- Print enabled built-in commands.
- Print disabled built-in commands.
- Print enabled POSIX special built-in commands.
- Print disabled POSIX special built-in commands.
- Print all POSIX special built-in commands.
- Load built-in commands from a dynamic library.
- Remove built-in commands loaded from a dynamic library.

#### Options

```shell
-a    Print all built-in commands, whether disabled or not.
-d    Remove built-in commands loaded from a dynamic library.
-n    Disable built-in commands or show disabled built-in commands.
-p    Print built-in commands in a reusable format.
-s    Display only enabled POSIX special built-in commands.
-f    Load built-in commands from a dynamic library.
-ns   Print disabled POSIX special built-in commands.
-as   Print all POSIX special built-in commands, whether disabled or not.
```

#### Parameters

filename: The dynamic library filename.

name (optional): Built-in command(s). Multiple names can be specified.

#### Return Value

`enable` returns success unless `name` is not a built-in command or an error occurs.

### Examples

```shell
# POSIX special built-ins
# Assuming no built-ins are disabled
# Disable two POSIX special built-ins
enable -n set source
# Print disabled POSIX special built-ins
enable -ns
# Print all POSIX special built-ins
enable -as
# Print enabled POSIX special built-ins
enable -s
```

```shell
# Assuming no built-ins are disabled
# Disable one or more built-in commands
enable -n echo pwd
# Print all built-in commands
enable -a
# Print enabled built-in commands
enable
# Print disabled built-in commands
enable -n
# Enable one or more built-in commands
enable pwd
```

### Q&A

Q: Where are the demonstrations for `-f`, `-d`, and `-p`?

A: Regarding `-f` and `-d`, suitable examples haven't been found yet. If you have better examples, feel free to submit a pull request. 
For the `-p` option, there seems to be no visible difference in output; you can compare `enable -p | cat -A` and `enable | cat -A` to check for invisible characters.

Q: Can I disable `enable` itself? Can I still enable/disable built-ins after that?

A: Yes, you can disable it. However, once disabled, you cannot use it to enable or disable any built-in commands until it is re-enabled (which usually requires a new shell session).

### Note

> When a Linux shell command is executed, the shell always looks for the command in its built-ins first. If found, it executes it. If not, it searches through the paths specified in the `$PATH` environment variable. It might seem like there's no way to override a shell built-in with a user-defined command. Fortunately, the `enable` command allows us to do exactly that.

1. Regarding command priority, refer to the "Note" section of the `builtin` command.

  When the built-in `echo` is not disabled, to call the external `echo` command, you must use the full path like `/usr/bin/echo`.

  When `echo` is disabled, the priority becomes:
  Function > External Command
  If no `echo` function exists, the external command will be called.

2. This is a bash built-in command. For more help, use the `help` command.
