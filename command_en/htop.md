htop
===

An interactive process viewer that allows dynamic observation of system processes.

## Description

The `htop` command is an interactive process viewer for Linux systems. It is a text-mode application (run in a console or X terminal) and requires the `ncurses` library.

Compared to the traditional `top` command, `htop` is more user-friendly. It allows interactive operations, supports color themes, enables horizontal and vertical scrolling of the process list, and supports mouse operations.

Advantages of `htop` over `top`:

- Scroll the process list horizontally and vertically to see all processes and complete command lines.
- Starts faster than `top`.
- No need to enter the PID to kill a process.
- Supports mouse operations.
- `top` is generally more cumbersome to use.

Disadvantages of `top`:

- Only supports keyboard operations.
- Display is relatively monotonous.

htop Official Website: http://htop.sourceforge.net/

### htop Installation

In most Linux distributions, `htop` is not pre-installed. However, as one of the most popular utilities, you can find it in the default repositories of almost every Linux distribution.

For Debian/Ubuntu-based systems:

```shell
sudo apt install htop
```

For Fedora:

```shell
sudo dnf install htop
```

For CentOS or RedHat:

```shell
sudo yum install htop
```

A Snap package is also available:

```shell
sudo snap install htop
```

If you are using other distributions or want to build from source, you can use `wget` to download and install. This requires `wget` and `cmake`.

```shell
wget https://github.com/htop-dev/htop/archive/refs/tags/3.2.2.tar.gz
tar -zxvf 3.2.2.tar.gz
cd htop-3.2.2/
./autogen.sh && ./configure
make
sudo make install
```

Refer to the [htop GitHub page](https://github.com/htop-dev/htop) for detailed instructions.

**Note**: By default, `htop` installs to `/usr/local`. To install to a different path, use the `--prefix` flag during configuration: `./configure --prefix=/some/path`.

### Syntax

```shell
htop
```

### Options

```shell
-C --no-color               Use a monochrome color scheme
-d --delay=DELAY            Set the delay between updates, in tenths of a second
-s --sort-key=COLUMN        Sort by column (try --sort-key=help for a list)
-u --user=USERNAME          Show only processes for a specified user
-p --pid=PID,[,PID,PID...]  Show only specific PIDs
-h --help                   Print help message
-v --version                Print version information
```

#### Examples

- `-C` option: Set the interface to no color.
- `-d` option: Set the refresh interval in seconds. For example, `htop -d 10` refreshes every 10 seconds.
- `-s` option: Sort by a specified column. For example, `htop -s PID` sorts the list by Process ID.
- `-u` option: Display process information for a specific user. For example, `htop -u test` shows only processes owned by the user "test".

### Interactive Commands

```shell
h, ?    F1: View htop help/manual
S       F2: Setup
/       F3: Search for a process
\       F4: Filter processes by keyword
t       F5: Tree view
<, >    F6: Select sorting method
[       F7: Decrease nice value (increase priority)
]       F8: Increase nice value (decrease priority)
k       F9: Kill selected process
q       F10: Quit htop

/ : Search characters
h : Show help
l : List open files for a process (requires lsof)
u : Show processes for a specific user
U : Untag all processes
s : Trace system calls with strace
t : Toggle tree view

H : Show/hide user threads
I : Invert sort order
K : Show/hide kernel threads    
M : Sort by memory usage
P : Sort by CPU usage    
T : Sort by running time

Up/Down or PgUp/PgDn: Move selection
Left/Right or Home/End: Scroll process list
Space: Tag/Untag a process (commands like "kill" apply to all tagged processes)
```

### htop Settings

Click "Setup" or press F2 to enter the `htop` configuration page.

#### 1. Meters
Configure display information at the top. It's divided into "Left column" and "Right column". Select items from "Available meters" and press F5 to add to the left or F6 to add to the right. You can choose display modes like LED, Bar, or Text.

#### 2. Display options
Select content to display. Press Space to toggle (x means selected). Press F10 to save.

#### 3. Colors
Set the interface color scheme.

#### 4. Columns
Add or remove columns. Use F7/F8 to move items up/down, F9 to remove, and F10 to save. You can add columns like PPID or PGRP based on your needs.

**F3 Search Process**
Press F3 or "/" to enter search mode. Type the process name, and matches will be highlighted.

**F4 Filter**
Case-insensitive fuzzy search. Only processes matching the keyword will be displayed.

**F5 Tree View**
Displays processes in a parent-child hierarchy.

**F6 Sort**
Choose the sorting criteria (e.g., CPU%, MEM%, PID).

**F7, F8 Adjust Nice Value**
F7 decreases the nice value (increases priority), and F8 increases it (decreases priority). Range is -20 to 19.

**F9 Kill Process**
Select a process and press F9 to send a signal (default is SIGTERM) to terminate it.

**F10 Quit**
Exit `htop`.
