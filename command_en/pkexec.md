pkexec
===

Executes a command as another user.

## Description

**pkexec** allows an authorized user to execute a PROGRAM as another user. If PROGRAM is not specified, the default shell will be run. If no username is specified, the program will be executed as the administrative superuser, `root`.

### Syntax

```shell
pkexec [--version] [--disable-internal-agent] [--help]
pkexec [--keep-cwd] [--user username] PROGRAM [ARGUMENTS...]
```

### Options

```text
PROGRAM: The program to run.
ARGUMENTS: Arguments passed to the program.

--version: Output version information and exit.
--disable-internal-agent: Avoid registering a textual authentication agent.
--help: Output help text and exit.
--keep-cwd: Keep the current working directory (default is /home/<username>/).
--user <username>: Execute the command as the specified user.
```

### Return Value

Upon successful completion, the return value is that of the PROGRAM.

- `127`: Authorization not obtained or an authentication error occurred.
- `126`: The user cancelled the authentication dialog.

### Examples

1.  **Run a command with administrative privileges:**

```bash
pkexec ls
```

2.  **Run a graphical command with administrative privileges:**

```bash
pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY command
```

3.  **Run a command as a specific user:**

```bash
pkexec --user username command
```

Note: When using `pkexec`, the system will prompt for the administrator's password. Use it only when necessary and exercise caution with administrative privileges.

### References
- [pkexec(1) — Linux manual page](https://man.archlinux.org/man/pkexec.1.en)
