rpmbuild
===

Create RPM binary packages and source packages.

## Description

The **rpmbuild command** is used to create RPM binary and source packages.

### Syntax

```shell
rpmbuild(options)
```

### Options

```shell
--initdb: Initialize the RPM database.
--rebuilddb: Rebuild the RPM database from installed package headers.
-ba: Create both binary and source packages.
-bb: Create binary packages.
-bs: Create source packages.
```

### Examples

```shell
rpmbuild -ba 'path_to_spec_file'
```

After building, binary RPM packages can be found under `/usr/src/redhat/RPMS/`, categorized by their corresponding CPU architecture (e.g., in the `/usr/src/redhat/RPMS/i386` directory). Source RPM packages can be found under `/usr/src/redhat/SRPMS/`; these are not categorized by architecture as they are source code.
