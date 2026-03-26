rpm
===

RPM package management tool.

## Description

The **rpm command** is a management tool for RPM packages. Originally, `rpm` was a program specifically used by the Red Hat Linux distribution to manage various Linux packages. Due to its adherence to GPL rules and its powerful, convenient features, it has become widely popular and gradually adopted by other distributions. The emergence of the RPM package management system has made Linux easier to install and upgrade, indirectly enhancing its applicability.

### Syntax

```shell
rpm(options)(parameters)
```

### Options

```shell
-a: Query all packages.
-b<stage><package_file>+ or -t <stage><package_file>+: Set the completion stage for packaging and specify the package filename.
-c: List only configuration files; this parameter must be used with the "-l" parameter.
-d: List only documentation files; this parameter must be used with the "-l" parameter.
-e<package> or --erase<package>: Delete the specified package.
-f<file>+: Query the package that owns the specified file.
-h or --hash: List hash marks during package installation.
-i: Display related information about the package.
-i<package_file> or --install<package_file>: Install the specified package file.
-l: Display the file list for the package.
-p<package_file>+: Query the specified RPM package file.
-q: Use query mode; for any issues, the rpm command will prompt the user first.
-R: Display dependency information for the package.
-s: Display file status; this parameter must be used with the "-l" parameter.
-U<package_file> or --upgrade<package_file>: Upgrade the specified package file.
-v: Display the execution process of the command.
-vv: Display the execution process in detail for troubleshooting.
```

### Parameters

Package: Specifies the RPM package to be operated on.

### Examples

**How to install an RPM package**

RPM package installation can be completed using the `rpm` program. Execute the following command:

```shell
rpm -ivh your-package.rpm
```

Where `your-package.rpm` is the name of the RPM package you want to install, generally located in the current directory.

During installation, the following warnings or prompts may appear:

```shell
... conflict with ...
```

This may mean that some files in the package to be installed would overwrite existing files. By default, installation will not proceed. You can use `rpm --force -i` to force the installation.

```shell
... is needed by ...
... is not installed ...
```

This indicates that some software required by this package is not installed. You can use `rpm --nodeps -i` to ignore this message. In other words, `rpm -i --force --nodeps` can ignore all dependencies and file issues, allowing any package to be installed. However, such a forced installation cannot guarantee full functionality.

**How to install a .src.rpm package**

Some packages end in `.src.rpm`. These packages contain source code and need to be compiled during installation. There are two methods to install these packages:

Method 1:

```shell
rpm -i your-package.src.rpm
cd /usr/src/redhat/SPECS
rpmbuild -bp your-package.specs             # A specs file with the same name as your package
cd /usr/src/redhat/BUILD/your-package/      # A directory with the same name as your package
./configure                                 # This step is the same as compiling normal source software
make
make install
```

Method 2:

```shell
rpm -i your-package.src.rpm
cd /usr/src/redhat/SPECS
```

The first two steps are the same as Method 1.

```shell
rpmbuild -bb your-package.specs       # A specs file with the same name as your package
```

At this point, in `/usr/src/redhat/RPM/i386/` (or i686, noarch, etc., depending on the package), there will be a new RPM package, which is the compiled binary.

Execute `rpm -i new-package.rpm` to complete the installation.

**How to uninstall an RPM package**

Use the command `rpm -e package_name`. The package name can include version information but cannot have the `.rpm` suffix. For example, to uninstall `proftpd-1.2.8-1`, you can use the following formats:

```shell
rpm -e proftpd-1.2.8-1
rpm -e proftpd-1.2.8
rpm -e proftpd-
rpm -e proftpd
```

The following formats are NOT allowed:

```shell
rpm -e proftpd-1.2.8-1.i386.rpm
rpm -e proftpd-1.2.8-1.i386
rpm -e proftpd-1.2
rpm -e proftpd-1
```

Sometimes errors or warnings may appear:

```shell
... is needed by ...
```

This indicates that this software is required by other software and cannot be uninstalled casually. You can use `rpm -e --nodeps` to force uninstallation.

**How to extract files from an RPM package without installing it**

Use the tools `rpm2cpio` and `cpio`:

```shell
rpm2cpio xxx.rpm | cpio -vi
rpm2cpio xxx.rpm | cpio -idmv
rpm2cpio xxx.rpm | cpio --extract --make-directories
```

The `i` and `extract` parameters are the same, meaning extract files. `v` indicates showing the execution process. `d` and `make-directory` are the same, meaning create directories based on the original paths of the files in the package. `m` means maintain the modification time of the files.

**How to view files and other information related to an RPM package**

All the following examples assume the use of the package `mysql-3.23.54a-11`.

1. What RPM packages are installed in my system?

```shell
rpm -qa # Lists all installed packages
```

To find all installed packages containing the string "sql":

```shell
rpm -qa | grep sql
```

2. How to get the full name of a package?

```shell
rpm -q mysql
```

This gets the full name of the `mysql` package installed in the system, from which you can obtain the current version and other information. In this example, you might get `mysql-3.23.54a-11`.

3. Where were the files in an RPM package installed?

```shell
rpm -ql package_name
```

Note that this is the package name without the `.rpm` suffix. If you only want to know where the executable programs are, you can also use `which`, for example:

```shell
which mysql
```

4. What files does an RPM package contain?

*   For an uninstalled package: `rpm -qlp ****.rpm`
*   For an installed package: `rpm -ql ****`

5. How to get version, purpose, and other related information about a package?

*   For an uninstalled package: `rpm -qip ****.rpm`
*   For an installed package: `rpm -qi ****`

6. Which package installed a certain program, or which package contains this program?

```shell
rpm -qf `which program_name`    # Returns the full name of the package
rpm -qif `which program_name`   # Returns information about the package
rpm -qlf `which program_name`   # Returns the file list of the package
```

Note: Use backticks (`` ` ``) for command substitution. You can also use `rpm -qilf` to output both package information and the file list.

7. Which package installed a certain file, or which package contains this file?

The previous method only applies to executable programs. The following method can be used for any file, provided you know its path. First, get the full path of the file (using `whereis` or `which`), then use `rpm -qf`:

```shell
whereis ftptop
ftptop: /usr/bin/ftptop /usr/share/man/man1/ftptop.1.gz

rpm -qf /usr/bin/ftptop
proftpd-1.2.8-1

rpm -qf /usr/share/doc/proftpd-1.2.8/rfc/rfc0959.txt
proftpd-1.2.8-1
```

## More Examples
> Library dependencies: http://rpmfind.net/

Source package -> Compilation -> Binary package (RPM package / Default system package)

RPM naming rules: Software (Name, Version) + System (OS Version, Architecture)
RPM verification: `SM5DLUGT` -> Size, Mode (type/permissions), MD5, Device, Link path, User, Group, Time (modified time)

YUM: Solves RPM dependency issues.

```shell
# rpm
mysql57-community-release-el6-8.noarch.rpm # An example of an RPM package name
/var/lib/rpm/ # Database mapping full package names to package names

rpm -Uivh --nodeps xxx # upgrade install verbose hash
rpm -qilpfa | grep xxx # query info list(file locations) package(rpm file) file(belongs to) all
rpm -e # erase (uninstall)
rpm -V # verify
rpm2cpio | cpio -idv

# Default RPM installation locations
/etc/           Configuration files
/usr/bin/       Executable files
/usr/lib/       Libraries used by programs
/usr/share/doc/ Documentation/Manuals
/usr/share/man/ Manual pages
```
