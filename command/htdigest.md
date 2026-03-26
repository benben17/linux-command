htdigest
===

A utility for creating and updating user authentication files for Apache.

## Supplemental Information

The **htdigest command** is a built-in utility for the Apache web server used to create and update the flat-files used to store usernames, realms, and passwords for digest authentication.

### Syntax

```shell
htdigest [options] passwdfile realm username
```

### Options

```shell
-c    # Create the passwdfile. If the file already exists, it is overwritten.
```

### Parameters

*   **passwdfile**: Specifies the path to the password file to be created or updated.
*   **realm**: Specifies the authentication realm to which the username belongs.
*   **username**: The username to create or update in the passwdfile.
