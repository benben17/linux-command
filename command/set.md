set
===

Display or set shell attributes and variables.

## Description

The **set command** is primarily used to display existing shell variables and set their values. When using `set` to modify shell attributes, the "+" and "-" signs are used to enable and disable specific modes, respectively. The `set` command cannot define new shell variables; use the `declare` command in the format `variable_name=value` to define new variables.

### Syntax

```shell
set [options] [parameters]
```

### Options

```shell
-a: Mark modified or created variables for export to the environment.
-b: Cause the status of terminated background jobs to be reported immediately.
-C: Prevent existing regular files from being overwritten by redirection.
-d: Shell uses a hash table to remember the locations of commands to speed up execution. Use -d to disable this.
-e: Exit immediately if a command exits with a non-zero status.
-f: Disable pathname expansion (globbing).
-h: Remember the location of functions as they are defined.
-H: Enable "!" style history substitution.
-k: All arguments in the form of assignment statements are placed in the environment for a command.
-l: Save and restore the binding of a name in a for loop.
-m: Enable job control (monitor mode).
-n: Read commands but do not execute them.
-p: Turn on privileged mode.
-P: If set, do not follow symbolic links when performing commands such as cd.
-t: Exit after reading and executing one command.
-u: Treat unset variables as an error when performing parameter expansion.
-v: Print shell input lines as they are read.
-x: Print commands and their arguments as they are executed.
```

### Parameters

Used to disable a previously set attribute.

### Examples

Use the `declare` command to define a new environment variable "mylove" and set its value to "Visual C++":

```shell
declare mylove='Visual C++'   # Define a new environment variable
```

Use the `set` command to export the newly defined variable to the environment:

```shell
set -a mylove                 # Set as an environment variable
```

After executing this command, the corresponding environment variable will be added. You can use the `env` and `grep` commands to display and search for the environment variable "mylove":

```shell
env | grep mylove             # Display the value of the environment variable
```

At this point, the command will output the value of the environment variable.
