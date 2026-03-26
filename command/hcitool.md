hcitool
===

`hcitool` is a Linux command-line tool used for managing and debugging Bluetooth devices. It can be used to scan for nearby Bluetooth devices, connect to them, and send HCI (Host Controller Interface) commands and data packets.

## Installation

`hcitool` is a standard Linux command-line utility and is typically pre-installed on most Linux distributions. If it is not installed, you can install it using the following command (example for Debian-based distributions):

```bash
sudo apt-get install bluez
```

## Usage
Note: Using Bluetooth Low Energy (BLE) related commands typically requires elevated privileges (e.g., `sudo hcitool lescan`).

### Syntax

`hcitool [options] <command> [command parameters]`

### Commands

```text
    dev     Display local devices
    inq     Inquire remote devices
    scan    Scan for remote devices
    name    Get name from remote device
    info    Get information from remote device
    spinq   Start periodic inquiry
    epinq   Exit periodic inquiry
    cmd     Submit arbitrary HCI commands
    con     Display active connections
    cc      Create a connection to a remote device
    dc      Disconnect from a remote device
    sr      Switch central/peripheral role
    cpt     Change connection packet type
    rssi    Display connection RSSI
    lq      Display link quality
    tpl     Display transmit power level
    afh     Display AFH channel map
    lp      Set/display link policy settings
    lst     Set/display link supervision timeout
    auth    Request authentication
    enc     Set connection encryption
    key     Change connection link key
    clkoff  Read clock offset
    clock   Read local or remote clock
    lescan  Start LE scan
    leinfo  Get LE remote information
    lealadd Add device to LE accept list
    lealrm  Remove device from LE accept list
    lealsz  Read size of LE accept list
    lealclr Clear LE accept list
```

### Common Examples

1. Scan for nearby Bluetooth devices:

`hcitool scan`

2. Connect to a Bluetooth device via its MAC address:

`hcitool cc <MAC_ADDRESS>`

3. Display information about local Bluetooth adapters:

`hcitool dev`

4. Retrieve the Bluetooth name for a specific MAC address:

`hcitool name <MAC_ADDRESS>`

5. Display current active Bluetooth connections:

`hcitool con`
