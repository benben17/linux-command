neofetch
===

A tool to display system information with a distribution logo

## Description

**neofetch** supports Linux/Unix, Windows, and macOS. It is integrated into the package repositories of most distributions and can be installed directly.

Neofetch is a tool that displays system information in the terminal alongside the distribution's logo. The `neofetch` command provides a brief summary of the system. Information displayed includes: Model, OS, Kernel, CPU, GPU, Memory, Uptime, Packages, Shell, Resolution, DE, WM, WM Theme, Theme, Icons, and Terminal.

Neofetch is an open-source tool. [Project Address](https://github.com/dylanaraps/neofetch)

### Installation

Debian/Ubuntu

```shell
sudo apt install neofetch -y
```

CentOS

```shell
sudo yum install neofetch -y
sudo dnf install neofetch -y
```

[More installation options](https://github.com/dylanaraps/neofetch/wiki/Installation)

### Syntax

```shell
neofetch
```

### Output Examples

macOS:
```shell
                    'c.          mac@Mac-mini.local
                 ,xNMM.          --------------------------
               .OMMMMo           OS: macOS 12.4 21F79 arm64
               OMMM0,            Host: Macmini9,1
     .;loddo:' loolloddol;.      Kernel: 21.5.0
   cKMMMMMMMMMMNWMMMMMMMMMM0:    Uptime: 2 hours, 57 mins
 .KMMMMMMMMMMMMMMMMMMMMMMMWd.    Packages: 20 (brew)
 XMMMMMMMMMMMMMMMMMMMMMMMX.      Shell: zsh 5.8.1
;MMMMMMMMMMMMMMMMMMMMMMMM:       Resolution: 2560x1440, 1920x1080
:MMMMMMMMMMMMMMMMMMMMMMMM:       DE: Aqua
.MMMMMMMMMMMMMMMMMMMMMMMMX.      WM: Quartz Compositor
 kMMMMMMMMMMMMMMMMMMMMMMMMWd.    WM Theme: Blue (Dark)
 .XMMMMMMMMMMMMMMMMMMMMMMMMMMk   Terminal: iTerm2
  .XMMMMMMMMMMMMMMMMMMMMMMMMK.   Terminal Font: Monaco 12
    kMMMMMMMMMMMMMMMMMMMMMMd     CPU: Apple M1
     ;KMMMMMMMWXXWMMMMMMMk.      GPU: Apple M1
       .cooc,.    .,coo:.        Memory: 2251MiB / 16384MiB
```

Ubuntu:

```shell
            .-/+oossssoo+/-.               root@root 
        `:+ssssssssssssssssss+:`           ------------ 
      -+ssssssssssssssssssyyssss+-         OS: Ubuntu 20.04.4 LTS aarch64 
    .ossssssssssssssssssdMMMNysssso.       Host: Firefly RK3568-ROC-PC HDMI (Linux) 
   /ssssssssssshdmmNNmmyNMMMMhssssss/      Kernel: 4.19.193 
  +ssssssssshmydMMMMMMMNddddyssssssss+     Uptime: 7 days, 13 hours, 3 mins 
 /sssssssshNMMMyhhyyyyhmNMMMNhssssssss/    Packages: 1158 (dpkg) 
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   Shell: bash 5.0.17 
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   Resolution: 1440x900 
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   WM: Openbox 
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   Theme: Arc-Darker [GTK3] 
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   Icons: Adwaita [GTK3] 
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   Terminal: /dev/pts/0 
 /sssssssshNMMMyhhyyyyhdNMMMNhssssssss/    CPU: Firefly RK3568-ROC-PC HDMI (Linux) (4) @ 1.992GHz 
  +sssssssssdmydMMMMMMMMddddyssssssss+     Memory: 617MiB / 7687MiB 
   /ssssssssssshdmNNNNmyNMMMMhssssss/
    .ossssssssssssssssssdMMMNysssso.                               
      -+sssssssssssssssssyyyssss+-                                 
        `:+ssssssssssssssssss+:`
            .-/+oossssoo+/-.
```
