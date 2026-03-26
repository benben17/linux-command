timedatectl
===

Used to set or query system time, date, and timezone configurations in Linux.

## Description

In Linux system administration, this command is commonly used to set or change the current date, time, and timezone, or to enable automatic system clock synchronization with remote NTP servers to ensure the Linux system always maintains the correct time.

## Synopsis

```shell
timedatectl [OPTIONS...] COMMAND ...
```

## Main Purpose

- Convert time to a selected format, defaulting to the current time.
- Set the system time.

## Parameters

```shell
Query or change system time and date settings.

  -h --help                Show help information.
     --version             Show package version.
     --no-pager            Do not pipe output to a pager.
     --no-ask-password     Do not prompt for password.
  -H --host=[USER@]HOST    Operate on a remote host.
  -M --machine=CONTAINER   Operate on a local container.
     --adjust-system-clock Adjust system clock when changing local RTC mode.
     --monitor             Monitor systemd-timesyncd status.
  -p --property=NAME       Show only the property with this name.
  -a --all                 Show all properties, including empty ones.
     --value               When showing properties, only print the value.

Commands:
  status                   Show current time settings.
  show                     Show systemd-timedated properties.
  set-time TIME            Set system time.
  set-timezone ZONE        Set system timezone.
  list-timezones           Show known timezones.
  set-local-rtc BOOL       Control whether RTC is in local time (BOOL can be 1/true or 0/false).
  set-ntp BOOL             Enable or disable network time synchronization (BOOL can be 1/true or 0/false).
  timesync-status          Show systemd-timesyncd status.
  show-timesync            Show systemd-timesyncd properties.
```

## Examples

Display system current time and date

```shell
$ timedatectl status
      Local time: Fri 2022-04-08 17:06:40 CST
  Universal time: Fri 2022-04-08 09:06:40 UTC
        RTC time: Fri 2022-04-08 17:04:02
       Time zone: Asia/Shanghai (CST, +0800)
     NTP enabled: n/a
NTP synchronized: no
 RTC in local TZ: yes
      DST active: n/a
```

Display systemd-timedated properties

```
$ timedatectl show
Timezone=Asia/Shanghai
LocalRTC=no
CanNTP=yes
NTP=yes
NTPSynchronized=yes
TimeUSec=Fri 2022-04-08 17:04:02 CST
RTCTimeUSec=Fri 2022-04-08 17:04:02 CST
```

Display all available system timezones

```shell
$ timedatectl list-timezones
Africa/Abidjan
Africa/Accra
Africa/Addis_Ababa
```

Set the local timezone from Shanghai (Asia/Shanghai) to Amsterdam (Europe/Amsterdam)

```shell
$ timedatectl set-timezone "Europe/Amsterdam"
```

Set the local timezone to Coordinated Universal Time (UTC)

```shell
$ timedatectl set-timezone UTC
```

Set system time (format: HH:MM:SS)

```shell
$ timedatectl set-time "07:25:46"
```

Set system date (format: YYYY-MM-DD)

```shell
$ timedatectl set-time "2021-12-12"
```

If only the date is set, the time will default to "00:00:00" (it is recommended to set both date and time)

```shell
$ timedatectl set-time "2021-12-12 07:25:46"
```

Set the hardware clock (RTC) to local time (not recommended; using UTC for RTC is more appropriate to avoid issues with timezone changes and Daylight Saving Time adjustments)

```shell
$ timedatectl set-local-rtc 1
```

Set the hardware clock (RTC) to Coordinated Universal Time (UTC)

```shell
$ timedatectl set-local-rtc 0
```

Enable NTP automatic time synchronization

```shell
$ timedatectl set-ntp true
```

Disable NTP automatic time synchronization

```shell
$ timedatectl set-ntp false
```

View the status of the systemd-timesyncd service

```shell
$ timedatectl timesync-status
       Server: 91.189.94.4 (ntp.ubuntu.com)
Poll interval: 17min 4s (min: 32s; max 34min 8s)
         Leap: normal
      Version: 4
      Stratum: 2
    Reference: 91EECB0E
    Precision: 1us (-23)
Root distance: 29.922ms (max: 5s)
       Offset: +2.497ms
        Delay: 199.540ms
       Jitter: 5.834ms
 Packet count: 6
    Frequency: +13.039ppm
```

`systemd-timedated` may default to Google's NTP servers (e.g., time1.google.com). For successful network time synchronization, you can edit the `/etc/systemd/timesyncd.conf` file to add your own NTP server addresses.
