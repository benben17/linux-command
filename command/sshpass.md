sshpass
===

Non-interactive SSH password provider

## Description

The **sshpass command** is a utility for non-interactive SSH password authentication. It should generally not be used on production servers for security reasons.

If you need to automatically provide a password and username at an SSH login prompt, `sshpass` can help. It is a simple, lightweight tool that provides a non-interactive way to handle password verification.

### Installation

```shell
# RedHat/CentOS
yum install sshpass

# Debian/Ubuntu
apt-get install sshpass
```

### Syntax

```shell
sshpass [option] command [arg ...]
```

### Options

```shell
Usage: sshpass [-f|-d|-p|-e] [-hV] command parameters
    -f filename: Read the password from the first line of the specified file.
    -d number: Use the specified file descriptor as the source for the password.
    -p password: Provide the password as an argument (insecure).
    -e: Read the password from the environment variable "SSHPASS".
    (If no argument is provided, the password is read from standard input.)

    -P prompt: Specify a prompt string for sshpass to detect the password request.
    -v: Verbose mode.
    -h: Display help.
    -V: Print version information.
Only one of -f, -d, -p, or -e can be used at a time.
```

### Examples

1. Pass password in plain text (**not recommended**):

```shell
sshpass -p 'my_pass_here' ssh aaronkilik@10.42.0.1 'df -h'
```

2. Pass password via a file:

```shell
sshpass -f password_filename ssh aaronkilik@10.42.0.1 'df -h'
```

3. Use the `SSHPASS` environment variable:

```shell
sshpass -e ssh aaronkilik@10.42.0.1 'df -h'
```

For more usage details, refer to [https://linux.cn/article-8086-1.html](https://linux.cn/article-8086-1.html).
