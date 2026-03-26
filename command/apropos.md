apropos
===

Search for strings in the whatis database

## Additional Information

The **apropos command** searches for keywords in specific database files containing short descriptions of system commands and sends the results to standard output.

If you don't know the name of the command required to complete a specific task, you can use a keyword to search for it using the Linux apropos utility. This utility searches for keywords and displays a short description of all man pages that contain matching items. Additionally, using the man utility with the -k (keyword) option yields the same results as using the Linux apropos utility (it is actually the same command).

### Syntax

```shell
apropos [-dalhvV] -e|-[w|-r] [-s section] [-m system[,...]] [-M path] [-L locale] -C [file] keyword ...
```

### Options

```shell
-d, --debug: Output debugging information.
-v, --verbose: Output detailed warning information.
-r, --regex: Interpret each keyword as a regular expression. This is the default behavior. Each keyword will match manual pages and descriptions.
-w, --wildcard: Interpret each keyword as a shell-style wildcard.
-e, --exact: Each keyword will exactly match the manual page name and description.
-a, --and: Only show manual pages and descriptions that match all keywords. By default, items matching any keyword are shown.
-l, --long: Do not trim output based on terminal width.
-s section, --section section: Only search the specified manual section.
-m system[,...], --systems=system[,...]: Used to find manual pages for other operating systems.
-M path, --manpath=path: Specify a colon-separated list of manual page hierarchies to search. The default is to use the $MANPATH environment variable. This option overrides the content of $MANPATH.
-L locale, --locale=locale: apropos calls the C function setlocale to get current localization information, including $LC_MESSAGES and $LANG. Use this option to provide a locale string to temporarily change localization information.
-C file, --config-file=file: Use this user configuration file instead of the default ~/.manpath.
-h, --help: Print help information and exit.
-V, --version: Print version information and exit.
```

### Return Value

Returns 0 for success, 1 for usage, syntax, or configuration file errors, 2 for operational errors, and 16 if no matches are found.

### Examples

```shell
[root@localhost ~]# man -k who
at.allow [at]        (5)  - determine who can submit jobs via at or batch
at.deny [at]         (5)  - determine who can submit jobs via at or batch
jwhois               (1)  - client for the whois service
jwhois              (rpm) - Internet whois/nicname client.
Net::LDAP::Extension::whoami (3pm)  - LDAP Who am I? Operation
w                    (1)  - Show who is logged on and what they are doing
who                  (1p)  - display who is on the system
who                  (1)  - show who is logged on
whoami               (1)  - print effective userid

[root@localhost ~]# apropos who
at.allow [at]        (5)  - determine who can submit jobs via at or batch
at.deny [at]         (5)  - determine who can submit jobs via at or batch
jwhois               (1)  - client for the whois service
jwhois              (rpm) - Internet whois/nicname client.
Net::LDAP::Extension::WhoAmI (3pm)  - LDAP Who am I? Operation
w                    (1)  - Show who is logged on and what they are doing
who                  (1p)  - display who is on the system
who                  (1)  - show who is logged on
whoami               (1)  - print effective userid
```

Search for manual pages that contain both "emacs" and "vi" in their names or descriptions:

```shell
apropos -a emacs vi
```
