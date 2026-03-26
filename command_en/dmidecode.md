dmidecode
===

DMI table decoder for Linux.

## Description

The **dmidecode** command allows you to retrieve hardware information on a Linux system. It works by decoding information in the DMI (Desktop Management Interface) table and displaying it in a human-readable text format. Since DMI information can be manually modified, the data may not always be perfectly accurate. `dmidecode` follows the SMBIOS/DMI standard, and its output includes information about the BIOS, system, motherboard, processor, memory, cache, and more.

DMI is a management system that helps collect computer system information. The collection of DMI information must strictly follow the SMBIOS specification. SMBIOS (System Management BIOS) is a unified specification that motherboard or system manufacturers must follow to display product management information in a standard format. SMBIOS and DMI are open technical standards drafted by the Desktop Management Task Force (DMTF), and DMI is designed to be applicable to any platform and operating system.

DMI acts as an interface between management tools and the system layers. It establishes standard manageable systems, making it easier for computer manufacturers and users to understand the system. The main component of DMI is the Management Information Format (MIF) database, which includes all information about the computer system and accessories. Through DMI, users can obtain serial numbers, computer manufacturers, serial port information, and other system accessory details.

### Syntax

```shell
dmidecode [options]
```

### Options

```shell
-d        (default: /dev/mem) Read information from a device file.
-h        Display help information.
-s        Only display the value of the DMI string identified by a keyword.
-t        Only display the entries of type.
-u        Do not decode the entries, display their hexadecimal dump instead.
--dump-bin file   Dump the DMI data to a binary file.
--from-dump FILE  Read DMI data from a binary file.
-V        Display version information.
```

 **dmidecode Keywords for String and Type:** 

(1) Valid string keywords:

*   bios-vendor
*   bios-version
*   bios-release-date
*   system-manufacturer
*   system-product-name
*   system-version
*   system-serial-number
*   system-uuid
*   baseboard-manufacturer
*   baseboard-product-name
*   baseboard-version
*   baseboard-serial-number
*   baseboard-asset-tag
*   chassis-manufacturer
*   chassis-type
*   chassis-version
*   chassis-serial-number
*   chassis-asset-tag
*   processor-family
*   processor-manufacturer
*   processor-version
*   processor-frequency

(2) Valid type keywords:

*   bios
*   system
*   baseboard
*   chassis
*   processor
*   memory
*   cache
*   connector
*   slot

(3) Complete list of type numbers:

*   BIOS
*   System
*   Base Board
*   Chassis
*   Processor
*   Memory Controller
*   Memory Module
*   Cache
*   Port Connector
*   System Slots
*   On Board Devices
*   OEM Strings
*   System Configuration Options
*   BIOS Language
*   Group Associations
*   System Event Log
*   Physical Memory Array
*   Memory Device
*   32-bit Memory Error
*   Memory Array Mapped Address
*   Memory Device Mapped Address
*   Built-in Pointing Device
*   Portable Battery
*   System Reset
*   Hardware Security
*   System Power Controls
*   Voltage Probe
*   Cooling Device
*   Temperature Probe
*   Electrical Current Probe
*   Out-of-band Remote Access
*   Boot Integrity Services
*   System Boot
*   64-bit Memory Error
*   Management Device
*   Management Device Component
*   Management Device Threshold Data
*   Memory Channel
*   IPMI Device
*   Power Supply
*   Additional Information
*   Onboard Device

### Examples

```shell
dmidecode -t 1  # View system information
dmidecode | grep 'Product Name' # View system model
dmidecode | grep 'Serial Number' # View motherboard serial number
dmidecode -t 2  # View motherboard information
dmidecode -s system-serial-number # View system serial number
dmidecode -t memory # View memory information
dmidecode -t 11 # View OEM information
dmidecode -t 17 # View memory device information
dmidecode -t 16 # View physical memory array information
dmidecode -t 4  # View CPU information

cat /proc/scsi/scsi # View hard disk information (alternative method)
```

Executing `dmidecode` without options usually outputs all hardware information. The `-t` option is very useful for filtering by type. For example, to get processor information:

```shell
[root@localhost ~]# dmidecode -t processor
# dmidecode 2.11
SMBIOS 2.5 present.

Handle 0x0001, DMI type 4, 40 bytes
Processor Information
        Socket Designation: Node 1 Socket 1
        Type: Central Processor
        Family: Xeon MP
        Manufacturer: Intel(R) Corporation
        id: C2 06 02 00 FF FB EB BF
        Signature: Type 0, Family 6, Model 44, Stepping 2
        Flags:
                FPU (Floating-point unit on-chip)
                VME (Virtual mode extension)
                DE (Debugging extension)
                PSE (Page size extension)
                TSC (time stamp counter)
                MSR (Model specific registers)
                PAE (Physical address extension)
                MCE (Machine check exception)
                CX8 (CMPXCHG8 instruction supported)
                APIC (On-chip APIC hardware supported)
                SEP (Fast system call)
                MTRR (Memory type range registers)
                PGE (Page global enable)
                MCA (Machine check architecture)
                CMOV (Conditional move instruction supported)
                PAT (Page attribute table)
                PSE-36 (36-bit page size extension)
                CLFSH (CLFLUSH instruction supported)
                DS (Debug store)
                ACPI (ACPI supported)
                MMX (MMX technology supported)
                FXSR (FXSAVE and FXSTOR instructions supported)
                SSE (Streaming SIMD extensions)
                SSE2 (Streaming SIMD extensions 2)
                ss (Self-snoop)
                HTT (Multi-threading)
                TM (Thermal monitor supported)
                PBE (Pending break enabled)
        Version: Intel(R) Xeon(R) CPU           E5620  @ 2.40GHz
        Voltage: 1.2 V
        External Clock: 5866 MHz
        Max Speed: 4400 MHz
        Current Speed: 2400 MHz
        Status: Populated, Enabled
        Upgrade: ZIF Socket
        L1 Cache Handle: 0x0002
        L2 Cache Handle: 0x0003
        L3 Cache Handle: 0x0004
        Serial Number: Not Specified
        Asset Tag: Not Specified
        Part Number: Not Specified
        Core Count: 4
        Core Enabled: 4
        Thread Count: 8
        Characteristics:
                64-bit capable

Handle 0x0055, DMI type 4, 40 bytes
Processor Information
        Socket Designation: Node 1 Socket 2
        Type: Central Processor
        Family: Xeon MP
        Manufacturer: Not Specified
        ID: 00 00 00 00 00 00 00 00
        Signature: Type 0, Family 0, Model 0, Stepping 0
        Flags: None
        Version: Not Specified
        Voltage: 1.2 V
        External Clock: 5866 MHz
        Max Speed: 4400 MHz
        Current Speed: Unknown
        Status: Unpopulated
        Upgrade: ZIF Socket
        L1 Cache Handle: Not Provided
        L2 Cache Handle: Not Provided
        L3 Cache Handle: Not Provided
        Serial Number: Not Specified
        Asset Tag: Not Specified
        Part Number: Not Specified
        Characteristics: None
```

Check the number of memory slots, used slots, and memory module sizes:

```shell
dmidecode | grep -P -A5 "Memory\s+Device" | grep Size | grep -v Range 

#   Size: 2048 MB
#   Size: 2048 MB
#   Size: 4096 MB
#   Size: No Module Installed
```

Check maximum supported memory capacity:

```shell
dmidecode | grep -P 'Maximum\s+Capacity'

#  Maximum Capacity: 16 GB
```

Check memory speed:

```shell
dmidecode | grep -A16 "Memory Device"

#   Memory Device
#     Array Handle: 0x1000
#     Error Information Handle: Not Provided
#     Total Width: 72 bits
#     Data Width: 64 bits
#     Size: 2048 MB
#     Form Factor: DIMM
#     Set: 1
#     Locator: DIMM_A1
#     Bank Locator: Not Specified
#     Type: DDR3
#     Type Detail: Synchronous Unbuffered (Unregistered)
#     Speed: 1333 MHz
#     Manufacturer: 00CE000080CE
#     Serial Number: 4830F3E1
#     Asset Tag: 01093200
#     Part Number: M391B5673EH1-CH9
#   --
#   Memory Device
#     Array Handle: 0x1000
#     Error Information Handle: Not Provided
#     Total Width: 72 bits
#     Data Width: 64 bits
#     Size: 2048 MB
#     Form Factor: DIMM
#     Set: 1
#     Locator: DIMM_A2
#     Bank Locator: Not Specified
#     Type: DDR3
#     Type Detail: Synchronous Unbuffered (Unregistered)
#     Speed: 1333 MHz
#     Manufacturer: 00AD000080AD
#     Serial Number: 1BA1F0B5
#     Asset Tag: 01110900
#     Part Number: HMT325U7BFR8C-H9
#   --

dmidecode | grep -A16 "Memory Device" | grep 'Speed'

#  Speed: 1333 MHz
#  Speed: 1333 MHz
#  Speed: 1333 MHz
#  Speed: Unknown
```
