source
===

Read and execute commands from a specified file in the current shell environment.

### Synopsis

source filename [arguments]

### Main Description

- Executes a file and loads variables and functions from the file into the current execution environment.

#### Parameters

filename: The file to be executed.

arguments (optional): Arguments passed to the file.

#### Return Value

`source` returns the exit status of the last command executed in the file, or failure if the file cannot be read.

#### Error Usage

- File not found in `$PATH`.
- File not provided.

### Examples

- During the execution of some tools, environment variables are exported to a file in the form of "export XXX=XXXXXX" or "declare XXX=XXXXXX". Then, `source` is used to load the content of that file into the execution environment.

- Read and execute the `/root/.bash_profile` file.

```shell
[root@localhost ~]# source ~/.bash_profile
```

### Q&A

Q: What is the difference between `source` and `sh` in terms of executing a file?

A: `sh` executes the file in a sub-shell, while `source` loads variables and functions from the executed file into the current terminal environment (excluding variables modified by `local` inside functions). You can refer to the **Knowledge Points** section of the `export` command.

### Note

1. This command is a bash built-in; for related help information, please check the `help` command.
