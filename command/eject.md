eject
===

Eject removable media.

## Description

The **eject** command is used to eject removable media. If the device is mounted, `eject` will unmount it before ejecting.

`eject` allows removable media (typically CD-ROMs, floppy disks, tapes, or JAZ and ZIP disks) to be ejected under software control. The command can also control some multi-disc CD-ROM changers, automatic eject features supported by some devices, and the closing of CD-ROM drive trays. The device corresponding to `name` will be ejected; `name` can be a device file or its mount point, a full path, or the device file name omitting the leading `/dev` or `/mnt`. If no name is specified, `cdrom` is used by default.

There are four different eject methods, depending on whether the device is a CD-ROM, SCSI device, removable floppy disk, or tape. The default behavior is to try all four methods in sequence until one succeeds. If the device is currently mounted, it will be unmounted before ejecting.

### Syntax

```shell
eject [options] [parameters]
```

### Options

```shell
-a <on|off> or --auto <on|off>: Control the auto-eject feature of the device.
-c <slot> or --changerslot <slot>: Select a disc from a CD-ROM changer.
-d or --default: Display the default device instead of performing an action.
-f or --floppy: Eject a floppy disk.
-h or --help: Display help.
-n or --noop: Display the selected device but do not eject.
-q or --tape: Eject a magnetic tape.
-r or --cdrom: Eject a CD-ROM.
-s or --scsi: Eject using SCSI commands.
-t or --trayclose: Close the CD-ROM tray.
-v or --verbose: Display detailed information during execution.
```

### Parameters

Device Name: Specify the name of the device to be ejected.
