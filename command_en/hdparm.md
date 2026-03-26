hdparm
===

Display and set hard drive parameters.

## Supplemental Information

The **hdparm command** provides a command-line interface for reading and setting parameters for IDE or SATA/SCSI hard drives.

### Syntax

```shell
hdparm (options) (parameters)
```

### Options

```shell
-a <count>: Set/get the sector count for filesystem readahead;
-A <0|1>: Disable/enable IDE drive look-ahead feature;
-c <mode>: Enable/disable IDE 32-bit I/O support;
-C: Check current IDE power mode status;
-d <0|1>: Disable/enable the DMA flag;
-f: Flush the buffer cache for the device on exit;
-g: Display drive geometry (cylinders, heads, sectors) and total sectors;
-h: Display help information;
-i: Display drive identification information provided at boot time;
-I: Request identification info directly from the drive;
-k <0|1>: Set/get keep_settings_over_reset flag;
-K <0|1>: Set/get drive keep_features_over_reset flag;
-m <count>: Set/get multiple sector count for multiple-sector I/O;
-n <0|1>: Set/get ignore-write-errors flag;
-p <mode>: Set IDE PIO mode;
-P <count>: Set the drive's internal prefetch count;
-q: Quiet operation;
-r <0|1>: Set/get the read-only flag for the device;
-S <timeout>: Set the standby (spindown) timeout for the drive;
-t: Perform device read timings;
-T: Perform cache read timings;
-u <0|1>: Set/get interrupt-unmask flag;
-v: Display all settings;
-w <0|1>: Set/get write-caching flag;
-X <mode>: Set the IDE transfer mode;
-y: Force an IDE drive to immediately enter the low power standby mode;
-Y: Force an IDE drive to immediately enter the lowest power sleep mode;
-Z: Disable the automatic power-saving function of certain Seagate drives.
```

### Parameters

Device: Specifies the device file corresponding to the hard drive (e.g., `/dev/sda`).

### Examples

Display hard drive settings:

```shell
hdparm /dev/sda
/dev/sda:
IO_support = 0 (default 16-bit)
readonly = 0 (off)
readahead = 256 (on)
geometry = 19457 [cylinders] / 255 [heads] / 63 [sectors], sectors = 312581808 [total], start = 0
```

Display drive geometry (cylinders, heads, sectors):

```shell
hdparm -g /dev/sda
/dev/sda:
geometry = 19457 [cylinders] / 255 [heads] / 63 [sectors], sectors = 312581808 [total], start = 0
```

Test drive read speed:

```shell
hdparm -t /dev/sda
/dev/sda:
 Timing buffered disk reads:  244 MB in  3.02 seconds =  80.82 MB/sec
```

Test cache read speed:

```shell
hdparm -T /dev/sda
/dev/sda:
 Timing cached reads:   4684 MB in  2.00 seconds = 2342.92 MB/sec
```

Check the power management mode of the drive:

```shell
hdparm -C /dev/sda
/dev/sda:
drive state is: standby
```

**Note: Hard drive bad sector repair methods**

```shell
Check: smartctl -l selftest /dev/sda
Unmount: umount /dev/sda*
Repair (using badblocks): badblocks /dev/sda
```
