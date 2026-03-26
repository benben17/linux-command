apt-get
===

APT package management tool in Debian Linux distributions

## Additional Information

**apt-get** is the APT package management tool in the Debian Linux distribution. All Debian-based distributions use this package management system. Deb packages bundle application files together, similar to installation files on Windows.

### Syntax

```shell
apt-get [OPTION] PACKAGE
```

### Options

```shell
apt-get install  # Install a new package
apt-get remove   # Uninstall an installed package (keep configuration files)
apt-get purge    # Uninstall an installed package (delete configuration files)
apt-get update   # Update the package list
apt-get upgrade  # Upgrade all installed packages
apt-get autoremove   # Uninstall unneeded package dependencies
apt-get dist-upgrade # Automatically handle package dependency upgrades
apt-get autoclean    # Remove .deb files of uninstalled packages from the disk
apt-get clean        # Remove all downloaded .deb files

-c: Specify the configuration file.
```

### Parameters

* Management command: Operations for APT package management.
* Package: The package to be manipulated.

### Examples

The first step in using `apt-get` is to import the necessary software repositories. Debian software repositories are collections of all Debian packages stored on public internet sites. By adding their addresses, `apt-get` can search for the software we want. `/etc/apt/sources.list` is the configuration file storing these address lists, formatted as follows:

```shell
deb web_or_ftp_address [distribution_name] main/contrib/non-free
```

Ubuntu, a commonly used Debian-based distribution, uses `apt-get` to retrieve this list. Here are some commonly used commands:

Run this command after modifying `/etc/apt/sources.list` or `/etc/apt/preferences`. Additionally, you should run this command regularly to ensure your package list is up to date:

```shell
apt-get update
```

Install a new package:

```shell
apt-get install packagename
```

Uninstall an installed package (keep configuration files):

```shell
apt-get remove packagename
```

Uninstall an installed package (delete configuration files):

```shell
apt-get --purge remove packagename
```

Downloaded packages are backed up on the disk. If you need space, you can use this command to delete the backup files for software you have already uninstalled:

```shell
apt-get autoclean
```

This command will also delete the backup files of installed software, but this will not affect the software's use:

```shell
apt-get clean
```

Upgrade all installed packages:

```shell
apt-get upgrade
```

Upgrade the system to a new version:

```shell
apt-get dist-upgrade
```

Run this command regularly to clear the .deb files of uninstalled packages. This way, you can free up a lot of disk space. If you need more space urgently, use `apt-get clean`. This command will delete the .deb files for all installed software packages as well. In most cases, you won't need these .deb files again, so if you're struggling with low disk space, this might be worth a try:

```shell
apt-get autoclean
```
