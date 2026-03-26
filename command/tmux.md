tmux
===

Tmux is an excellent terminal multiplexer, similar to GNU Screen but originating from OpenBSD and licensed under BSD.

## Description

The most intuitive benefit of using it is that after logging in to a remote host through a terminal and running tmux, you can open multiple consoles within it without "wasting" extra terminals to connect to the remote host.

Enable mouse wheel scrolling:
`ctrl+b`, press colon `:` to enter command-line mode, then type `set -g mouse on` and press Enter.

## Features

- Provides a powerful and easy-to-use command-line interface.
- Supports horizontal and vertical window splitting.
- Panes can be moved and resized freely, or you can use one of the four preset layouts.
- Supports UTF-8 encoding and 256-color terminals.
- Copy and paste across multiple buffers.
- Select windows, sessions, and clients via an interactive menu.
- Supports searching across windows.
- Supports automatic and manual window locking.

## Installation

```shell
# On macOS, install via brew
brew install tmux
# On Ubuntu, install directly via apt-get
sudo apt-get install tmux
# On CentOS 7, install directly via yum
yum install -y tmux

# On CentOS 6, manual compilation is required
yum install libevent libevent-devel ncurses-devel
tar -zvxf tmux-2.3.tar.gz # (Download beforehand: wget https://github.com/tmux/tmux/releases/download/2.3/tmux-2.3.tar.gz)
cd tmux-2.3
./configure
make && make install
```

## Shortcut Usage Guide

| Shortcut | Description |
| :----- | :--------------------------- |
| Ctrl+b | Activate the console; subsequent keys take effect after this |


### System Operations

| Shortcut | Description |
| :----- | ------------------------------------------------------------ |
| ?      | List all shortcuts; press q to return |
| d      | Detach from current session; you can return to the Shell and use `tmux attach` to re-enter |
| D      | Select a session to detach; used when multiple sessions are open |
| Ctrl+z | Suspend current session |
| r      | Force redraw of a non-detached session |
| s      | Select and switch session; used when multiple sessions are open |
| :      | Enter command-line mode; you can input supported commands, e.g., `kill-server` to stop the server |
| [      | Enter copy mode; operations are similar to vi/emacs, press q/Esc to exit |
| ~      | List prompt message buffer; contains various messages previously returned by tmux |


### Window Operations

| Shortcut | Description |
| :----- | ------------------------------------ |
| c      | Create a new window |
| &      | Close current window |
| Digit  | Switch to the specified window |
| p      | Switch to the previous window |
| n      | Switch to the next window |
| l      | Switch between the last two windows |
| w      | Switch window via window list |
| ,      | Rename current window for easier identification |
| .      | Change current window number (reorder windows) |
| f      | Find specified text in all windows |

### Pane Operations

| Shortcut | Description |
| :---------- | ------------------------------------------------------------ |
| ”           | Split current pane horizontally into two |
| %           | Split current pane vertically into two |
| x           | Close current pane |
| !           | Move current pane to a new window |
| Ctrl+Arrow  | Resize current pane by 1 cell |
| Alt+Arrow   | Resize current pane by 5 cells |
| Space       | Cycle through preset pane layouts (even-horizontal, even-vertical, main-horizontal, main-vertical, tiled) |
| q           | Display pane numbers |
| o           | Select the next pane in the current window |
| Arrow Keys  | Move cursor to select pane |
| {           | Swap current pane with previous one |
| }           | Swap current pane with next one |
| Alt+o       | Rotate panes in the current window counter-clockwise |
| Ctrl+o      | Rotate panes in the current window clockwise |


1) After entering the tmux panel, you must first press `ctrl+b`, release it, and then press other key combinations.
2) Frequently used combinations:

```shell
ctrl+b ?        # Display shortcut help
ctrl+b Space    # Use next built-in layout; interesting for displaying multiple screens vertically
ctrl+b !        # Turn current pane into a new window
ctrl+b  "       # Split window horizontally
ctrl+b %        # Split window vertically
ctrl+b q        # Show pane numbers
ctrl+b o        # Jump to next pane; switch between multiple screens
ctrl+b Arrows   # Previous and next pane
ctrl+b C-Arrows # Resize pane
ctrl+b &        # Exit current tmux after confirmation
ctrl+b [        # Copy mode: moves current screen to previous position, all others move forward
ctrl+b c        # Create new window
ctrl+b n        # Select next window
ctrl+b l        # Last used window
ctrl+b p        # Select previous window
ctrl+b w        # Display and select window via menu
ctrl+b s        # Display and select session via menu; commonly used to choose which tmux to enter
ctrl+b t        # Show clock; press Enter to return to shell
ctrl+b d        # Detach current session; return to Shell and use `tmux attach` to re-enter
```

## References

- Tmux Official Site: http://tmux.github.io/
