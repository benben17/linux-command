startx
===

Used to start X Window

## Description

The **startx command** is used to start X Window. In reality, the program that starts X Window is `xinit`.

### Syntax

```shell
startx (parameters)
```

### Parameters

* Client and options: X client and its options.
* Server and options: X server and its options.

### Examples

To start an X session on a workstation or X terminal, enter:

```shell
startx
```

To force start an X session on a workstation, enter:

```shell
startx -w
```

To start an X session for an X terminal and log out the user's telnet session, enter:

```shell
startx; kill -9 $
```

To start an X session using a `.xinitrc` script, enter:

```shell
startx -x .xinitrc
```

To start an X session using the `mwm` window manager, enter:

```shell
startx -m mwm
```

However, if a startup script file is found, the `-w` option is ignored. In the startup script, it is the user's responsibility to start the window manager, load X resources, and spawn X clients. Below is an example of a `.xsession` script:

```shell
#!/bin/csh
 (mwm &)
 xrdb -load .Xdefaults
 (xclock -g 75x75+0+0 &)
 (xbiff -g 75x75+101-0 &)
 if ("/dev/lft*" == "`tty`") then
  aixterm -g 80x24+0+0 +ut -C -T `hostname`
 else
  aixterm -g 80x24+0+0 +ut -T `hostname`
 endif
```

For workstations, the last line in the startup script should be a foreground `aixterm` command with the `-C` option for console messages. For X terminals, the last line should be a foreground `aixterm` command without the `-C` option. Additionally, since some X terminals do not terminate the telnet session when closed, users must exit the current telnet session before switching to the X session using a hotkey.

The `xdm` command in the `/usr/lib/X11/xdm/Xsession` file can also use the `startx` command. This provides the `xdm` command with the functionality of the `startx` command.

The following are file names consistently used to start X sessions:

```shell
$HOME/.xerrors     File where startx redirects error messages. By default, startx redirects errors to the .xerrors file in the user's home directory.
$HOME/.Xinit,  
$HOME/.xinit,  
$HOME/.Xinitrc,  
$HOME/.xinitrc,  
$HOME/.xsession    Acts as a "startup file" containing shell commands to start the window manager, load X resources, and spawn X clients.
$HOME/.Xdefaults,  
$HOME/.xresources  Acts as a loaded X resource file to set user preferences for X clients.
$HOME/.mwmrc       mwm configuration file.
$HOME/.twmrc       twm configuration file.
$HOME/.awmrc       awm configuration file.
$HOME/.uwmrc       uwm configuration file.
/dev/lft*          Interface for terminal or tty, workstation initial login shell.
```
