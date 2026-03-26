clock
===

Used to adjust RTC (Real Time Clock) time

## Description

The **clock command** is used to adjust the RTC time. RTC is the hardware clock built into the computer. Executing this command can display the current time, adjust the hardware clock, synchronize the system time with the hardware clock, or save the system time back to the hardware clock.

### Syntax

```shell
clock [--adjust][--debug][--directisa][--getepoch][--hctosys][--set --date="<datetime>"]
[--setepoch --epoch=<year>][--show][--systohc][--test][--utc][--version]
```

### Options

```shell
--adjust: The first time "--set" or "--systohc" is used to set the hardware clock, an adjtime file is created in the /etc directory. When these parameters are used again, the file records the difference between adjustments. Subsequent executions with "--adjust" will automatically calculate the average drift based on these values and adjust the hardware clock.
--debug: Display detailed information about the command execution, useful for troubleshooting.
--directisa: Tell the clock command not to use the /dev/rtc device file and instead access the hardware clock directly. This is suitable for older computers with only an ISA bus structure.
--getepoch: Output the hardware clock epoch value from the kernel to standard output.
--hctosys: Hardware Clock to System Time. Set the system time to match the hardware clock. Since this action updates access times for all files, it is best performed during system startup.
--set --date="<datetime>": Set the date and time of the hardware clock.
--setepoch --epoch=<year>: Set the hardware clock epoch value in the kernel, using a four-digit year.
--show: Read the hardware clock time and output it to standard output.
--systohc: System Time to Hardware Clock. Save the system time back into the hardware clock.
--test: Test mode only; do not actually write time to the hardware clock or system time.
--utc: Treat the hardware clock time as Coordinated Universal Time (UTC), also known as CUT or UCT.
--version: Display version information.
```

### Examples

Get the current time:

```shell
clock # Get the current time
```

Display UTC time:

```shell
clock --utc # Display UTC time
```
