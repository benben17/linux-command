lilo
===

Install the LInux LOader (LILO) boot manager

## Description

The **lilo** command is used to install the core boot loader, LILO (LInux LOader). LILO is a boot loader for Linux systems that manages the boot process. When executed alone, it reads the `/etc/lilo.conf` configuration file and installs LILO based on its contents.

LILO has become a standard component of many Linux distributions. As one of the older Linux boot loaders, it has evolved over time with community support and continues to serve as a functional modern boot loader. It includes features such as an enhanced user interface and the ability to leverage new BIOS features to bypass the original 1024-cylinder limit.

While LILO continues to evolve, its fundamental principles remain the same.

### Syntax

```shell
lilo (options)
```

### Options

```shell
-b <device>: Specify the device where LILO should be installed;
-c: Use compact map mode;
-C <config_file>: Specify the LILO configuration file;
-d <delay>: Set the boot delay time;
-D <label>: Specify the default OS or kernel label to boot;
-f <geom_file>: Specify the disk geometry configuration file;
-i <boot_sector>: Specify the boot sector file to use (default is /boot/boot.b);
-I <label>: Display the location of the specified kernel;
-l: Generate linear sector addresses;
-m <map_file>: Specify the map file;
-P <fix/ignore>: Decide whether to fix or ignore partition table errors;
-q: List the mapped kernel files;
-r <root_dir>: Set the directory to be mounted as root at boot;
-R <command>: Set a command to be executed first on the next boot;
-s <backup_file>: Specify the backup file;
-S <backup_file>: Force specify the backup file;
-t: Test mode; list actions without executing them;
-u <device>: Uninstall LILO;
-U <device>: Similar to -u but without timestamp checking;
-v: Verbose output;
-V: Display version information.
```

### Examples

**Using LILO as a Boot Loader**

Using LILO depends on whether you are performing a clean install or switching an existing system to LILO. For a clean install, refer to the "Configuring LILO" section. If you already have a Linux distribution installed, you can usually install and configure LILO to manage the boot process.

To migrate an existing Linux system to LILO, you must first obtain the latest version of LILO. It is strongly recommended to have a Linux boot disk handy in case of configuration errors. Once LILO is installed, making it take over the MBR is simple. Run the following as root:

```shell
/sbin/lilo -v -v
```

This will use the current LILO defaults and overwrite the MBR. Please read the "Configuring LILO" section to ensure it boots as expected. Also, if you want to run both Windows and Linux, it is recommended to install Windows first, followed by Linux, so that LILO is not overwritten by the Windows boot loader. Unlike LILO, most Windows boot loaders do not support booting Linux. If Linux is already installed, create a boot disk so you can restore the MBR after installing Windows.

**Configuring LILO**

LILO configuration is handled via the `/etc/lilo.conf` file. Below is an example configuration for a dual-boot machine with Linux and Windows:

- Windows XP is installed on the primary HDD (/dev/hda).
- Red Hat Linux is installed on the secondary HDD; the root partition is at /dev/hdb3.

Example `lilo.conf`:

```shell
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=100
compact
default=Linux
image=/boot/vmlinuz-2.4.18-14
	label=Linux
	root=/dev/hdb3
	read-only
	password=linux
other=/dev/hda
	label=WindowsXP
```

Configuration Option Descriptions:

*   `boot=`: Tells LILO where to install the boot loader (e.g., the MBR of the first hard drive).
*   `map=`: Points to the map file used internally by LILO during boot. This is generated automatically by `/sbin/lilo`. Do not modify this file!
*   `install=`: Points to the files LILO uses during the boot process (containing both primary and secondary boot loader parts). Do not modify this!
*   `prompt`: Tells LILO to use a user interface (in this example, offering Linux and WindowsXP).
*   `timeout=`: The time (in tenths of a second) to wait before booting the default OS.
*   `compact`: Speeds up the boot process by merging consecutive disk read requests.
*   `default=`: Specifies the default image to boot.
*   `image=`: Specifies the kernel version to boot.
*   `label=`: The label for the OS in the boot menu.
*   `root=`: Tells LILO where the root filesystem is located.
*   `read-only`: Mounts the root filesystem as read-only initially.
*   `password=`: Sets a password for the specific OS. Note: This is stored in plain text in `lilo.conf`.
*   `other=`: Similar to `image` and `root` but for non-Linux operating systems.

Many other parameters can be used in `lilo.conf`. Refer to the manual page (`man lilo.conf`) for more information. Since `lilo.conf` is not read at boot time, you must run `/sbin/lilo -v -v` to update the MBR whenever you change the configuration.

**Initial Boot Process**

When LILO boots, it prints the letters "L-I-L-O" in sequence. If all letters appear, the first stage of the boot was successful. Any missing letters indicate an issue:

- **L**: First-stage boot loader loaded. If it stops here, there is an issue loading the second stage (often a media issue or incorrect disk parameters).
- **LI**: Second-stage boot loader loaded but cannot be executed. May be due to a corrupt or moved `boot.b` file.
- **LIL**: Second-stage boot loader executing. May be an issue with the map file or descriptor table.
- **LIL?**: Loaded to the same stage as above but with an incorrect address.
- **LIL-**: Error loading the descriptor table.
- **LILO**: Successful load.

**Additional Boot Configurations**

Once LILO loads, you will see a prompt. Depending on the `timeout` setting, it will boot the default OS or wait for input. Pressing TAB will list available OS options.

Note that LILO does not support interactive configuration during boot; options must be specified in `lilo.conf` or when running `/sbin/lilo`.

One final tip: using a floppy boot disk for initial LILO testing is safer than modifying the hard drive's MBR directly. Set `boot=/dev/fd0` in `lilo.conf` for testing. Once everything works, switch it back to `boot=/dev/hda` and run `/sbin/lilo` one last time.
