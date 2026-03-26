aptitude
===

Package management tool in Debian Linux systems

## Additional Information

Like `apt-get`, the **aptitude command** is an extremely powerful package management tool in Debian Linux and its derivatives. Unlike `apt-get`, `aptitude` is better at handling dependency issues. For example, when removing a package, `aptitude` will also remove the packages it depends on if they are no longer needed. This ensures that no useless packages remain in the system, keeping it cleaner. It manages packages through both a text-based menu and command-line options.

### Syntax

```shell
aptitude (options) (parameters)
```

### Options

```shell
-h: Display help information;
-d: Download packages only, do not install;
-P: Ask for confirmation at every step;
-y: Answer "yes" to all questions;
-v: Display additional information;
-u: Download new package lists at startup.
```

### Parameters

Command: Operation commands for package management.

### Examples

Here are some commonly used `aptitude` commands:

```shell
aptitude update            # Update the list of available packages
aptitude upgrade           # Upgrade available packages
aptitude dist-upgrade      # Upgrade the system to a new distribution
aptitude install pkgname   # Install a package
aptitude remove pkgname    # Remove a package
aptitude purge pkgname     # Remove a package and its configuration files
aptitude search string     # Search for a package
aptitude show pkgname      # Show detailed information about a package
aptitude clean             # Delete downloaded package files
aptitude autoclean         # Delete only expired package files
```

You can also use `aptitude` in text-interface mode.
