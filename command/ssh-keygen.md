ssh-keygen
===

Authentication key generation, management, and conversion for SSH

## Description

The **ssh-keygen command** is used to generate, manage, and convert authentication keys for `ssh`. It supports both RSA and DSA authentication keys.

### Syntax

```shell
ssh-keygen [option]
```

### Options

```shell
-b: Specify the number of bits in the key to create.
-e: Read an OpenSSH private or public key file and print it in a specified format.
-C: Provide a new comment.
-f: Specify the filename of the key file.
-i: Read an unencrypted SSH-v2 compatible private or public key file and display an OpenSSH compatible key on stdout.
-l: Show the fingerprint of the specified public key file.
-N: Provide a new passphrase.
-P: Provide the (old) passphrase.
-q: Silence ssh-keygen.
-t: Specify the type of key to create.
-y: Read a private OpenSSH format file and print an OpenSSH public key to stdout.
```
