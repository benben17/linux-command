dnf
===

Next-generation RPM package manager.

## Description

**DNF** is the next-generation version of the RPM package manager. it first appeared in Fedora 18. Recently, it replaced YUM and officially became the package manager for Fedora 22.

The DNF package manager overcomes some bottlenecks of the YUM package manager, improving user experience, memory usage, dependency analysis, running speed, and more. DNF uses RPM, libsolv, and hawkey libraries for package management operations. Although it is not pre-installed in CentOS and RHEL 7, you can use DNF alongside YUM.

The latest stable version of DNF is 1.0, released on May 11, 2015. This version (and all previous versions) is mostly written in Python and licensed under GPL v2.

### Installing DNF Package Manager

DNF is not installed by default in RHEL or CentOS 7, but Fedora 22 uses DNF by default.

1. To install DNF, you must first install and enable the `epel-release` dependency.

Execute the following command:

```shell
yum install epel-release
```

or

```shell
yum install epel-release -y
```

There is no strict reason to use `-y` here; instead, without `-y`, users can see exactly what is being installed. For users without this need, you can use the `-y` parameter in YUM to install everything automatically.

2. Use the YUM command with the `epel-release` dependency to install the DNF package:

```shell
yum install dnf
```

Then, the DNF package manager is successfully installed on your system. Now, let's start with 27 common commands for the DNF package manager!

**Check DNF Version**

Purpose: View the version of the DNF package manager installed on your system.

```shell
dnf --version
```

**View Available DNF Repositories**

Purpose: Display the DNF repositories available in the system.

```shell
dnf repolist
```

**View All Available and Disabled DNF Repositories**

Purpose: Display all available and disabled DNF repositories in the system.

```shell
dnf repolist all
```

**List All RPM Packages**

Purpose: List all available packages from repositories and all packages already installed on the system.

```shell
dnf list
```

**List All Installed RPM Packages**

Purpose: List all installed RPM packages.

```shell
dnf list installed
```

**List All Available RPM Packages for Installation**

Purpose: List all packages available for installation from all enabled repositories.

```shell
dnf list available
```

**Search for an RPM Package in Repositories**

Purpose: Search for a package when you don't know its exact name. You need to type part of the software name after the `search` parameter. (In this example, we use "nano").

```shell
dnf search nano
```

**Find the Provider of a Specific File**

Purpose: Find which package provides a specific file in the system. (In this example, we find the provider of `/bin/bash`).

```shell
dnf provides /bin/bash
```

**View Package Details**

Purpose: View detailed information about a package before installing it. (In this example, we view details for "nano").

```shell
dnf info nano
```

**Install a Package**

Purpose: Automatically install the specified software and all its required dependencies. (In this example, we install "nano").

```shell
dnf install nano
```

**Upgrade a Package**

Purpose: Upgrade a specific package. (In this example, we upgrade "systemd").

```shell
dnf update systemd
```

**Check for System Package Updates**

Purpose: Check for updates for all packages in the system.

```shell
dnf check-update
```

**Upgrade All System Packages**

Purpose: Upgrade all packages in the system that have available updates.

```shell
dnf update
# or
dnf upgrade
```

**Remove a Package**

Purpose: Remove a specified package from the system. (In this example, we remove "nano").

```shell
dnf remove nano
# or
dnf erase nano
```

**Remove Unused Orphaned Packages**

Purpose: Automatically remove packages that were installed to satisfy dependencies but are no longer needed.

```shell
dnf autoremove
```

**Remove Cached Temporary Files**

Purpose: Remove various outdated files and uncompleted compilation projects left over during the use of DNF.

```shell
dnf clean all
```

**Get Help for a Specific Command**

Purpose: Get help on how to use a specific command, including available parameters and descriptions. (In this example, we get help for the "clean" command).

```shell
dnf help clean
```

**View All DNF Commands and Their Purposes**

Purpose: List all DNF commands and what they do.

```shell
dnf help
```

**View DNF Execution History**

Purpose: View the history of DNF commands executed on your system. This allows you to know what software has been installed or uninstalled since you started using DNF.

```shell
dnf history
```

**View All Package Groups**

Purpose: List all package groups.

```shell
dnf grouplist
```

**Install a Package Group**

Purpose: Install a specific package group. (In this example, we install "Educational Software").

```shell
dnf groupinstall 'Educational Software'
```

**Upgrade Packages in a Group**

Purpose: Upgrade software within a specific package group. (In this example, we upgrade "Educational Software").

```shell
dnf groupupdate 'Educational Software'
```

**Remove a Package Group**

Purpose: Remove a specific package group. (In this example, we remove "Educational Software").

```shell
dnf groupremove 'Educational Software'
```

**Install a Specific Software from a Specific Repository**

Purpose: Install a specific package from a specific repository. (In this example, we install "phpmyadmin" from the "epel" repository).

```shell
dnf --enablerepo=epel install phpmyadmin
```

**Synchronize Packages to the Latest Stable Release**

Purpose: Update all installed packages to the latest stable release from all available sources.

```shell
dnf distro-sync
```

**Reinstall a Specific Package**

Purpose: Reinstall a specific package. (In this example, we reinstall "nano").

```shell
dnf reinstall nano
```

**Downgrade a Specific Package Version**

Purpose: Lower the version of a specific package if possible. (In this example, we downgrade "acpid").

```shell
dnf downgrade acpid
```

Sample output:

```shell
Using metadata from Wed May 20 12:44:59 2015
No match for available package: acpid-2.0.19-5.el7.x86_64
Error: Nothing to do.
```

Original author's note: When executing this command, DNF did not downgrade the specified software ("acpid") as expected. This issue has been reported.

### Summary

As an upgrade and replacement for YUM, DNF can automate more operations. However, in my opinion, DNF might not be as popular among experienced Linux administrators for several reasons:

1. DNF does not have the `--skip-broken` command, and there is no alternative.
2. DNF lacks the `resolvedep` command used to determine which package provides a specific dependency.
3. DNF lacks the `deplist` command used to list a package's dependencies.
4. When you exclude a repository in DNF, it affects all subsequent operations, unlike in YUM where exclusions only apply during upgrades and installations.
