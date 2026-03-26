grub2-set-default
===

Set the default boot entry for GRUB2.

## Syntax

```shell
Usage: grub2-set-default [OPTION] MENU_ENTRY
Set the default boot menu entry for GRUB.
This requires setting GRUB_DEFAULT=saved in /etc/default/grub.

  -h, --help              print this message and exit
  -v, --version           print the version information and exit
  --boot-directory=DIR    expect GRUB images under the directory DIR/grub2
                          instead of the /boot/grub2 directory

MENU_ENTRY is a number, a menu item title or a menu item identifier.

Report bugs to <bug-grub@gnu.org>.
```

## Examples

View the available system kernels:

```shell
# awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
CentOS Linux (5.4.219-1.el7.elrepo.x86_64) 7 (Core)
CentOS Linux (3.10.0-1160.76.1.el7.x86_64) 7 (Core)
CentOS Linux (3.10.0-862.el7.x86_64) 7 (Core)
CentOS Linux (0-rescue-3221d376917c458992a952d6327f2d6a) 7 (Core)
```

The index for `grub2-set-default` starts from 0. To set the first entry as the default:

```shell
# grub2-set-default 0
```

To set the third entry (CentOS Linux 3.10.0-862...) as the default, change 0 to 2.

Reboot the system:

```shell
~]# init 6
```
