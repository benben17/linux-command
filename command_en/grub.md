grub
===

The command-line shell tool for the GRUB (GRand Unified Bootloader) multi-boot loader.

## Supplemental Information

The **grub command** is the command-line shell interface for the legacy GRUB bootloader.

### Syntax

```shell
grub [options]
```

### Options

```shell
--batch: Enable batch mode;
--boot-drive=<drive>: Specify the stage2 boot drive;
--config-file=<file>: Specify the stage2 configuration file;
--device-map=<file>: Specify the device map file;
--help: Display help information;
--install-partition=<partition>: Specify the stage2 installation partition;
--no-config-file: Do not use a configuration file;
--no-pager: Do not use the internal pager;
--preset-menu: Use a preset menu;
--probe-second-floppy: Probe the second floppy drive;
--read-only: Read-only mode.
```

### Examples

Using the `grub` command to boot a damaged Linux system. This is useful when the system cannot boot automatically, for example, when the screen shows only a `grub>` prompt but the data on the hard drive is intact.

In the `grub>` shell, you can manually boot the system using four main commands: `root`, `kernel`, `initrd`, and `boot`.

1. Type `root (hd` and press TAB twice to list possible disk devices (e.g., `hd0`, `hd1`).
2. Select the disk where Linux is installed (e.g., `hd0`) and type `root (hd0, ` then press TAB twice to list partitions. You can identify the Linux partition (type 0x83).
3. Select the partition containing the `/boot` directory, e.g., `root (hd0, 1)`, and press Enter.
4. Type `cat /boot/vm` and press TAB twice. If files starting with `vmlinuz-` appear, this is likely the `/boot` partition.
5. Check for the ramdisk image: `cat /boot/initrd` followed by TAB twice.
6. Check for the root partition: `cat /sbin/init` followed by TAB twice. If found, this is the `/` partition. If not, retry with another `root (hd0, N)` partition until you find `/sbin/init`.

Once the partitions are identified, execute the following:

```shell
root (hd0,1)                                           # Assume /dev/hda2 is the /boot partition
kernel /boot/vmlinuz-2.6.15-26-386 ro root=/dev/hda3   # Assume /dev/hda3 is the / partition
initrd /boot/initrd.img-2.6.15-26-386
boot
```

This will boot the system.

### References

- Free Software Foundation - GRUB Documentation: <https://www.gnu.org/software/grub/>
