lsusb
===

List USB devices

## Description

The **lsusb command** is used to display information about USB buses in the system and the devices connected to them. It is a helpful tool for USB driver development and identifying USB devices.

### Syntax

```shell
lsusb [OPTION]...
```

### Options

```shell
-v：Display detailed information about USB devices.
-s [[bus]:][devnum]：Show only devices on a specified bus and/or with a specified device number.
-d [vendor]:[product]：Show only devices with the specified vendor and product ID.
-t：Dump the physical USB device hierarchy as a tree.
-V：Display version information.
```

### Examples

Example output after inserting a USB mouse:

```shell
Bus 005 Device 001: id 0000:0000 
Bus 001 Device 001: ID 0000:0000 
Bus 004 Device 001: ID 0000:0000 
Bus 003 Device 001: ID 0000:0000 
Bus 002 Device 006: ID 15d9:0a37 
Bus 002 Device 001: ID 0000:0000 
```

**Explanation:**

*   **Bus 005**: Represents the 5th USB host controller (you can check all controllers using `lspci | grep USB`).
*   **Device 006**: The device number (devnum) assigned by the system to the USB mouse. In this example, it is connected to the 2nd USB host controller.
    *   Corresponding sysfs path: `/sys/devices/pci0000:00/0000:00:1d.1/usb2/2-2/devnum`
*   **ID 15d9:0a37**: The USB device ID (vendor:product). This ID is set by the chip manufacturer and uniquely identifies the device type.
    *   Vendor ID (15d9): `usb_device_descriptor.idVendor`
    *   Product ID (0a37): `usb_device_descriptor.idProduct`
    *   Sysfs paths: `/sys/devices/pci0000:00/0000:00:1d.1/usb2/2-2/idVendor` and `idProduct`

**Bus 002 Device 006: ID 15d9:0a37**
**Bus 002 Device 001: ID 0000:0000**

This indicates two devices on USB bus 002:
*   A USB root hub (Device 001).
*   A USB mouse (Device 006).
