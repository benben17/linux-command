lsb_release
===

Display LSB (Linux Standard Base) information

## Description

LSB stands for Linux Standard Base. The **lsb_release command** is used to display LSB and specific distribution version information. If used without parameters, it defaults to the `-v` parameter.

### Options

```shell
-v, --version      Show version information.
-i, --id           Show distribution ID.
-d, --description  Show distribution description.
-r, --release      Show release number of the distribution.
-c, --codename     Show distribution codename.
-a, --all          Show all of the above information.
-h, --help         Show help message.
-s, --short        Display short output (supported on RedHat and Fedora).
```

If the current distribution is LSB compatible, the `/etc/lsb-release` file (or files in `/etc/lsb-release.d/`) will contain the LSB_VERSION field. This field's value may be a series of supported module names separated by colons.

The optional fields include DISTRIB_ID, DISTRIB_RELEASE, DISTRIB_CODENAME, and DISTRIB_DESCRIPTION, which can override the content in `/etc/distrib-release` (where `distrib` is replaced by the distribution name).

The general format is `Distributor release x.x (Codename)`. Note: Debian systems lack corresponding description information (see `/etc/debian-version`); to support Debian, most information is added to the lsb-release file.
