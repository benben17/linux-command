ssh-add
===

Adds private key identities to the authentication agent (ssh-agent)

## Description

The **ssh-add command** adds private keys to the `ssh-agent` cache. The command is located at `/usr/bin/ssh-add`.

### Syntax

```shell
ssh-add [-cDdLlXx] [-t life] [file ...]
ssh-add -s pkcs11
ssh-add -e pkcs11
```

### Options

```shell
-D: Delete all identities from the agent.
-d: Remove identity from the agent.
-e pkcs11: Remove keys provided by the PKCS#11 shared library.
-s pkcs11: Add keys provided by the PKCS#11 shared library.
-L: List public key parameters of all identities currently represented by the agent.
-l: List fingerprints of all identities currently represented by the agent.
-t life: Set a maximum lifetime when adding identities to an agent. After this time, the identity will be automatically removed.
-X: Unlock the agent.
-x: Lock the agent with a password.
```

### Examples

1. Add a private key to the `ssh-agent` cache:

```shell
ssh-add ~/.ssh/id_dsa
```

2. Remove a key from `ssh-agent`:

```shell
ssh-add -d ~/.ssh/id_xxx.pub
```

3. List keys currently in `ssh-agent`:

```shell
ssh-add -l
```
