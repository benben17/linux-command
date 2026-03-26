yum
===

RPM-based package manager

## Description

**yum** (Yellowdog Updater, Modified) is an RPM-based package manager used in Fedora, Red Hat Enterprise Linux (RHEL), and CentOS. It allows system administrators to interactively and automatically update and manage RPM packages. It can automatically download RPM packages from specified servers and install them, handling dependencies automatically and installing all required software packages at once, eliminating the need to download and install them manually one by one.

yum provides commands to search, install, and delete specific, grouped, or all packages, with a syntax that is simple and easy to remember.

### Syntax

```shell
yum [options] [parameters]
```

### Options

```shell
-h, --help: Display help information;
-y, --assumeyes: Answer "yes" to all questions;
-c, --config=[config file]: Specify the configuration file;
-q, --quiet: Quiet mode;
-v, --verbose: Verbose mode;
-d, --debuglevel=[level]: Set the debug level (0-10);
-e, --errorlevel=[level]: Set the error level (0-10);
-R, --randomwait=[time]: Set the maximum wait time for yum to process a command;
-C, --cacheonly: Run entirely from the cache, without downloading or updating any header files.
```

### Parameters

```shell
install: Install RPM packages;
update: Update RPM packages;
check-update: Check if updates are available for RPM packages;
remove: Remove specified RPM packages;
list: List information about packages;
search: Search for package information;
info: Display descriptions and summaries for specified RPM packages;
clean: Clean up expired yum cache;
shell: Enter the yum shell prompt;
resolvedep: Show dependencies for RPM packages;
localinstall: Install local RPM packages;
localupdate: Update local RPM packages;
deplist: List all dependencies for RPM packages;
provides: Query which package contains a specific program.
```

### Examples

Some commonly used commands include:

*   Automatically search for the fastest mirror plugin: `yum install yum-fastestmirror`
*   Install the yum graphical window plugin: `yum install yumex`
*   View the list of groups available for batch installation: `yum grouplist`

**Installation**

```shell
yum install              # Install all available updates (if no package specified)
yum install package1     # Install a specific package 'package1'
yum groupinstall group1   # Install a program group 'group1'
```

**Updates and Upgrades**

```shell
yum update               # Update all packages
yum update package1      # Update a specific package 'package1'
yum check-update         # Check for available updates
yum upgrade package1     # Upgrade a specific package 'package1'
yum groupupdate group1   # Upgrade a program group 'group1'
```

**Search and Display**

```shell
# Check if MySQL is installed
yum list installed | grep mysql
yum list installed mysql*

yum info package1      # Display information for package 'package1'
yum list               # List all installed and available packages
yum list package1      # Show installation status for package 'package1'
yum groupinfo group1   # Show information for group 'group1'
yum search string      # Search for packages matching 'string'
```

**Removing Programs**

```shell
yum remove | erase package1   # Remove package 'package1'
yum groupremove group1         # Remove program group 'group1'
yum deplist package1           # View dependencies for package 'package1'
```

**Cleaning Cache**

```shell
yum clean packages       # Clear cached packages
yum clean headers        # Clear cached headers
yum clean oldheaders     # Clear old cached headers
```

**More Examples**

```shell
# yum configuration
/etc/yum.repos.d/       # Directory for yum repository configuration files
vi /etc/yum.repos.d/nginx.repo # Example: nginx yum repository
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/6/$basearch/
gpgcheck=0
enabled=1

# yum mirror configuration
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
wget https://mirror.tuna.tsinghua.edu.cn/help/centos/
yum makecache

# Adding language support
LANG=C # Original language
LANG=zh_CN.utf8 # Switch to Chinese
yum groupinstall "Chinese Support" # Add Chinese language support
```
