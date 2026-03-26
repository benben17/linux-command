smartmontools
===

Smartmontools is a hard drive testing tool that controls and manages the SMART (Self-Monitoring, Analysis, and Reporting Technology) system on hard drives.

## Installation

```shell
sudo aptitude install smartmontools
```

## Syntax

```shell
smartctl (option) (parameter)
```

## Options
```shell
-i <device>: Display identification information for the hard drive.
-a <device>: Display all SMART information for the device.
-H <device>: Display the health status of the device.
-A <device>: Display SMART vendor-specific attributes and values.
```

## Parameter
Hard drive device: Specify the hard drive to view (use `fdisk -l` to find available hard drive devices).

```shell
~ sudo fdisk -l
Device          Start      End          Sectors   Size Type
/dev/sda1     2048   1050623   1048576   512M EFI System
/dev/sda2  1050624 976771071 975720448 465.3G Linux filesystem
```

## Examples

Check the health status of the `/dev/sda1` drive. In this command, the `-s on` flag enables the SMART feature on the specified device. If SMART is already enabled on `/dev/sda`, you can omit it.
(PASSED means healthy; FAILED means failure is imminent, so you should start backing up important data from this disk.)

```shell
~ sudo smartctl -s on -H /dev/sda1   

=== START OF READ SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED
```

View specific attributes and values of the `/dev/sda1` drive.
(Power_On_Hours: Indicates a total powered-on time of 18,195 hours.)

```shell
~ sudo smartctl -A /dev/sda1

=== START OF READ SMART DATA SECTION ===
SMART Attributes Data Structure revision number: 16
Vendor Specific SMART Attributes with Thresholds:
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
  3 Spin_Up_Time            0x0023   100   100   002    Pre-fail  Always       -       1326
  4 Start_Stop_Count        0x0032   100   100   000    Old_age   Always       -       3752
  9 Power_On_Hours          0x0032   055   055   000    Old_age   Always       -       18195
 10 Spin_Retry_Count        0x0033   174   100   030    Pre-fail  Always       -       0
 12 Power_Cycle_Count       0x0032   100   100   000    Old_age   Always       -       3118
183 Runtime_Bad_Block       0x0032   100   100   001    Old_age   Always       -       0
184 End-to-End_Error        0x0033   100   100   097    Pre-fail  Always       -       0
185 Unknown_Attribute       0x0032   100   100   001    Old_age   Always       -       65535
187 Reported_Uncorrect      0x0032   001   001   000    Old_age   Always       -       134
188 Command_Timeout         0x0032   100   098   000    Old_age   Always       -       48
191 G-Sense_Error_Rate      0x0032   100   100   000    Old_age   Always       -       2850
192 Power-Off_Retract_Count 0x0022   100   100   000    Old_age   Always       -       32047593
193 Load_Cycle_Count        0x0032   095   095   000    Old_age   Always       -       51738
194 Temperature_Celsius     0x0022   060   055   040    Old_age   Always       -       40 (Min/Max 16/44)
```

### Running at specified intervals and notifying test results
First, edit the smartctl configuration file (`/etc/default/smartmontools`) to start `smartd` at system boot and specify the interval in seconds (e.g., 7200 = 2 hours).

```shell
start_smartd=yes
smartd_opts="--interval=7200"
```

Next, edit the `smartd` configuration file (`/etc/smartd.conf`) and add the following line:

```shell
/dev/sda -m myemail@mydomain.com -M test
```

Option descriptions:
-m: Specify an email address to send test reports to. This can be a system user like root, or an external email address like myemail@mydomain.com if the server is configured to send external emails.
-M: Specify the desired type of email report.
once: Send only one warning email for each type of disk problem detected.
daily: Send an additional warning reminder email every other day for each type of disk problem detected.
diminishing: Send an additional warning reminder email for each type of problem detected, starting every other day, then every two days, every four days, and so on. Each interval is twice the previous one.
test: Send a test email immediately as soon as `smartd` starts.
exec PATH: Instead of the default mail command, run the executable at PATH. PATH must point to an executable binary or script. When a problem is detected, you can specify an action to perform (flash console, shut down system, etc.).

Save the changes and restart `smartd`.
