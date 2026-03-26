pacman
===

The default package manager for Arch Linux and its derivatives.

## Installation

When installing Arch Linux, you are required to install the `base` package group, which includes `pacman`. For detailed Arch Linux installation procedures, please refer to the [Arch Wiki](https://wiki.archlinux.org/title/Installation_guide).

## Examples

### Install Packages
Official packages:
```bash
pacman -S p7zip
```

Unofficial packages (User-made, e.g., via AUR):
```bash
yay -S package_name1 package_name2 ...
```

### Search for Packages
Search the remote repositories:
```bash
pacman -Ss package_name1 package_name2 ...
```

### List All Installed Packages
```bash
pacman -Q
```

### Remove a Package
Remove a specific package:
```bash
pacman -R p7zip
```

Remove a package and its dependencies (which are not required by any other packages):
```bash
pacman -Rsc p7zip
```

### System Upgrade
Perform a full system upgrade (rolling release):
```bash
pacman -Syu
```

## References

- Arch Linux Wiki: [Pacman](https://wiki.archlinux.org/title/Pacman)
