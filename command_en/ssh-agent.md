ssh-agent
===

OpenSSH authentication agent

## Description

The **ssh-agent command** is a program that holds private keys used for public key authentication. It is typically started at the beginning of an X session or a login session, and all other windows or programs are started as clients that connect to it. Using environment variables, the agent can be located and used to automatically authenticate when logging into other machines using SSH.

Essentially, `ssh-agent` is a key manager. After running `ssh-agent`, use `ssh-add` to provide your private keys to it. Other programs needing authentication can then delegate the authentication process to `ssh-agent`.

### Syntax

```shell
ssh-agent [-c | -s] [-d] [-a bind_address] [-t life] [command [arg ...]]
ssh-agent [-c | -s] -k
```

### Options

```shell
-a bind_address: Bind the agent to the UNIX-domain socket `bind_address`.
-c: Generate C-shell style command output.
-d: Debug mode.
-k: Kill the current agent process.
-s: Generate Bourne shell style command output.
-t life: Set a default value for the maximum lifetime of identities added to the agent.
```

### Examples

Run `ssh-agent`:

```shell
ssh-agent
```

Running `ssh-agent` will print the environment variables it uses.
