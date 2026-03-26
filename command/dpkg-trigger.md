dpkg-trigger
===

A package trigger utility for Debian.

## Description

The **dpkg-trigger** command is a tool to explicitly activate triggers and check for their support in the running `dpkg`.

### Syntax

```shell
dpkg-trigger (options) (parameters)
```

### Options

```shell
--check-supported    Check if the running dpkg supports triggers. Returns 0 if supported.
--help               Display help information.
--admindir=<dir>     Change the location of the dpkg database.
--no-act             Test only, do not actually perform any actions.
--by-package=<pkg>   Override the trigger waiter.
```

### Parameters

Trigger Name: Specifies the name of the trigger.
