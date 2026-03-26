write
===

Send a message to another user

## Description

The **write command** is used to send a message to another user currently logged into the system. You can interactively type your message, and once you are finished, sending an EOF (usually `Ctrl+D`) will end the session and deliver the message. If the recipient is logged into more than one terminal, you can specify the terminal ID to send the message to.

### Syntax

```shell
write <user> [terminal]
```

### Parameters

```shell
user: The login name of the recipient.
terminal: The terminal name (e.g., pts/2) if the user is logged into multiple terminals.
```

### Examples

Send a message to Rollaend (who is only logged in once):

```shell
write Rollaend
```

Then type your message. Use `Ctrl+D` to send/finish.

Send a message to Rollaend's specific terminal (e.g., `pts/2`):

```shell
write Rollaend pts/2
```

Then type your message.

Note: If the recipient has set `mesg n`, they will not receive your message.
