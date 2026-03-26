cdrecord
===

Record audio or data Compact Discs from a command line.

## Description

The **cdrecord command** is used for burning optical discs in Linux systems, supporting both CD and DVD formats. Linux systems typically come with the `cdrecord` software installed.

### Syntax

```shell
cdrecord [options] [parameters]
```

### Options

```shell
-v: Show the detailed process of burning the disc.
-eject: Eject the disc after burning is complete.
speed=<burning_speed>: Specify the speed for burning the disc.
dev=<device_id>: Specify the device ID of the burner found using the "-scanbus" parameter.
-scanbus: Scan for available burners in the system.
```

### Parameters

ISO file: Specify the ISO image file to be used for burning the disc.

### Examples

View all CD-R(w) devices in the system:

```shell
cdrecord -scanbus
scsibus0:
  0,0,0     0) *
  0,1,0     1) *
  0,2,0     2) *
  0,3,0     3) 'HP      ' 'CD-Writer+ 9200 ' '1.0c' Removable CD-ROM
```

Burn a disc using an ISO file:

```shell
cdrecord -v -eject speed=4 dev=0,3,0 backup.iso
```

Parameter explanation:

* -v: Show the detailed process of burning the disc.
* -eject: Automatically eject the disc after burning.
* speed=4 dev=0,3,0: Burn at 4x speed to the HP CD-writer device.

Blank a rewritable disc:

```shell
cdrecord --dev=0,3,0 --blank=fast
```
