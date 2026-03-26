ncdu
===

Interactive disk usage analyzer, regarded as an enhanced version of du

## Description

**ncdu** (**NC**urses **D**isk **U**sage) is a disk usage analyzer for Unix-like systems, based on ncurses. It is an enhanced version of the traditional `du` command. Unlike the static text output of `du`, **ncdu provides an interactive TUI interface**, allowing you to browse the directory tree with arrow keys, sort results, view file information, and delete files directly.

It is ideal for quickly locating large files and analyzing disk space usage. Version 1.09 and later support exporting scan results as JSON.

### Official Resources

*   Official Website: [https://dev.yorhel.nl/ncdu](https://dev.yorhel.nl/ncdu)
*   Wikipedia: [https://en.wikipedia.org/wiki/Ncdu](https://en.wikipedia.org/wiki/Ncdu)

### Installation

**ncdu** is typically not pre-installed by default on most Linux distributions, but it is available in almost all major official repositories.

#### **Debian/Ubuntu**

```shell
sudo apt install ncdu
```

#### **CentOS / Rocky / AlmaLinux**

```shell
sudo yum install epel-release
sudo yum install ncdu
```

#### **Fedora**

```shell
sudo dnf install ncdu
```

#### **Arch Linux**

```shell
sudo pacman -S ncdu
```

#### **macOS (Homebrew)**

```shell
brew install ncdu
```

#### **FreeBSD**

```shell
pkg install ncdu
```

### Syntax

```shell
ncdu [options] [directory]
```

### Options

```shell
-h, --help             Display help information.
-v, --version          Display version information.
-x                     Stay on one file system (don't cross mount points).
-q                     Quiet mode: reduce screen refresh rate (useful for SSH).
-o FILE                Export scan results to FILE (JSON format, requires 1.09+).
-f FILE                Load scan results from a JSON FILE (requires 1.09+).
--exclude PATTERN      Exclude files or directories matching the pattern.
--exclude-from FILE    Read exclude patterns from a file.
--follow-symlinks      Follow symbolic links.
--confirm-deletion     Ask for confirmation before deleting a file.
```

### Interactive Commands

↑, ↓, →, ← represent arrow keys.

| Key           | Function                                          |
| ------------- | ------------------------------------------------- |
| ↑ / k         | Move cursor up                                    |
| ↓ / j         | Move cursor down                                  |
| → / Enter / l | Open the selected directory                       |
| ← / h         | Go back to the parent directory                   |
| n             | Sort by name (press again to toggle asc/desc)     |
| s             | Sort by size (press again to toggle asc/desc)     |
| d             | Delete selected item                              |
| g             | Toggle display of percentages and/or graph        |
| t             | Toggle directory-first sorting                    |
| c             | Toggle display of child item counts               |
| b             | Open a shell in the current directory             |
| i             | View detailed information for the selected item   |
| r             | Refresh/rescan the current directory              |
| q             | Exit ncdu                                         |

### Examples

#### Scan the current directory

```shell
ncdu
```

#### Scan a specific directory (e.g., /var/log)

```shell
ncdu /var/log
```

#### Export scan results to JSON (1.09+)

```shell
ncdu -o result.json /
```

#### Load results from a JSON file

```shell
ncdu -f result.json
```
