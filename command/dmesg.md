dmesg
===

Display or control the kernel ring buffer.

## Description

The **dmesg** command is used to examine or control the kernel ring buffer. The kernel stores boot-up messages in this ring buffer. If you miss the messages during boot, you can use `dmesg` to view them later. Boot messages are also saved in the `/var/log/dmesg` file.

### Syntax

```shell
dmesg (options)
```

### Options

```shell
-c          Clear the ring buffer after printing its contents.
-s <size>   Set the size of the buffer used to query the kernel ring buffer. The default is 8196.
-n <level>  Set the level at which logging of messages is done to the console.
```

### Examples

```shell
[root@localhost ~]# dmesg | head
Linux version 2.6.18-348.6.1.el5 (mockbuild@builder17.centos.org) (gcc version 4.1.2 20080704 (Red Hat 4.1.2-54)) #1 SMP Tue May 21 15:34:22 EDT 2013
BIOS-provided physical RAM map:
 BIOS-e820: 0000000000010000 - 000000000009f400 (usable)
 BIOS-e820: 000000000009f400 - 00000000000a0000 (reserved)
 BIOS-e820: 00000000000f0000 - 0000000000100000 (reserved)
 BIOS-e820: 0000000000100000 - 000000007f590000 (usable)
 BIOS-e820: 000000007f590000 - 000000007f5e3000 (ACPI NVS)
 BIOS-e820: 000000007f5e3000 - 000000007f5f0000 (ACPI data)
 BIOS-e820: 000000007f5f0000 - 000000007f600000 (reserved)
 BIOS-e820: 00000000e0000000 - 00000000e8000000 (reserved)
```

View basic hard disk information:

```shell
dmesg | grep sda

[    2.442555] sd 0:0:0:0: [sda] 488281250 512-byte logical blocks: (250 GB/232 GiB)
[    2.442590] sd 0:0:0:0: [sda] Write Protect is off
[    2.442592] sd 0:0:0:0: [sda] Mode Sense: 00 3a 00 00
[    2.442607] sd 0:0:0:0: [sda] Write cache: enabled, read cache: enabled, doesn't support DPO or FUA
[    2.447533]  sda: sda1
[    2.448503] sd 0:0:0:0: [sda] Attached SCSI disk
```

Search for multiple keywords:

```shell
dmesg | grep -E "vcc5v0_host|vcc_3v3_s0|ttyS"

[    1.193143] vcc5v0_host: supplied by vcc5v0_usb
[    1.481139] feb80000.serial: ttyS5 at MMIO 0xfeb80000 (irq = 73, base_baud = 1500000) is a 16550A
[    1.513541] vcc_3v3_s0: supplied by vcc5v0_sys
```
