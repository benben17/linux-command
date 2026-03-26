apt-key
===

Manage package keys in Debian Linux systems

## Additional Information

The **apt-key command** is used to manage package keys in Debian Linux systems. Each released deb package is authenticated via a key, and `apt-key` is used to manage these keys.

### Syntax

```shell
apt-key [command]
```

### Parameters

Management Command: APT key operation command.

### Examples

```shell
apt-key list          # List keys saved in the system.
apt-key add keyname   # Add the downloaded key to the local trusted database.
apt-key del keyname   # Delete the key from the local trusted database.
apt-key update        # Update the local trusted database and remove expired/useless keys.
```
