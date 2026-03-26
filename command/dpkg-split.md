dpkg-split
===

Split Debian packages into smaller parts.

## Description

The **dpkg-split** command is used to split large Debian software packages into smaller parts and can also reassemble the split parts.

### Syntax

```shell
dpkg-split (options) (parameters)
```

### Options

```shell
-S <bytes>      Set the maximum size for each split part (in bytes).
-s              Split the package.
-j <part> <part> ... Join split parts together.
-I <part>       Display information about a split part.
-l              List parts that do not match.
-discard <file> Discard parts that do not match.
```

### Parameters

Package: Specifies the ".deb" package to be split.

### Examples

Split `foo.deb` into multiple parts with a size of 460KB each:

```shell
dpkg-split -s foo.deb
```

Join split parts:

```shell
dpkg-split -j "foo*"
```
