date
===

Display or set system time and date

## Synopsis

```shell
date [OPTION]... [+FORMAT]
date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
```

## Description

- Convert time to a selected format, default is current time.
- Set the system time.

## Parameters

format: Output time format.

```shell
The following escape sequences are available for format:

%%      A literal %
%a      Locale's abbreviated weekday name (e.g., Sun)
%A      Locale's full weekday name (e.g., Sunday)
%b      Locale's abbreviated month name (e.g., Jan)
%B      Locale's full month name (e.g., January)
%c      Locale's date and time (e.g., Thu Mar  3 23:05:25 2005)
%C      Century; like %Y, except omit last two digits (e.g., 20)
%d      Day of month (e.g., 01)
%D      Date; same as %m/%d/%y
%e      Day of month, space padded; same as %_d
%F      Full date; same as %+4Y-%m-%d
%g      Last two digits of year of ISO week number
%G      Year of ISO week number; normally useful only with %V
%h      Same as %b
%H      Hour (00..23)
%I      Hour (01..12)
%j      Day of year (001..366)
%k      Hour, space padded ( 0..23); same as %_H
%l      Hour, space padded ( 1..12); same as %_I
%m      Month (01..12)
%M      Minute (00..59)
%n      A newline
%N      Nanoseconds (000000000..999999999)
%p      Locale's equivalent of either AM or PM; blank if not known
%P      Like %p, but lower case
%q      Quarter of year (1..4)
%r      Locale's 12-hour clock time (e.g., 11:11:04 PM)
%R      24-hour hour and minute; same as %H:%M
%s      Seconds since 1970-01-01 00:00:00 UTC
%S      Second (00..60)
%t      A tab
%T      Time; same as %H:%M:%S
%u      Day of week (1..7); 1 is Monday
%U      Week number of year, with Sunday as first day of week (00..53)
%V      ISO week number, with Monday as first day of week (01..53)
%w      Day of week (0..6); 0 is Sunday
%W      Week number of year, with Monday as first day of week (00..53)
%x      Locale's date representation (e.g., 12/31/99)
%X      Locale's time representation (e.g., 23:13:48)
%y      Last two digits of year (00..99)
%Y      Year
%z      +hhmm numeric time zone (e.g., -0400)
%:z     +hh:mm numeric time zone (e.g., -04:00)
%::z    +hh:mm:ss numeric time zone (e.g., -04:00:00)
%:::z   Numeric time zone with : to necessary precision (e.g., -04, +05:30)
%Z      Alphabetic time zone abbreviation (e.g., EDT)

By default, date pads numeric fields with zeroes. The following optional flags may follow '%':

-      (hyphen) Do not pad the field.
_      (underscore) Pad with spaces.
0      (zero) Pad with zeros.
+      Pad with zeros, and place '+' before future years with >4 digits.
^      Use upper case if possible.
#      Use opposite case if possible.

After any flags comes an optional field width, as a decimal number; then an optional modifier, which is either E to use the locale's alternate representations if available, or O to use the locale's alternate numeric symbols if available.
```

## Options

```shell
Long options are mandatory for short options too.

-d, --date=STRING          Display time described by STRING, not 'now'.
--debug                    Annotate the parsed date, and send warnings to stderr.
-f, --file=DATEFILE        Like --date; read lines from DATEFILE.
-I[FMT], --iso-8601[=FMT]  Output date/time in ISO 8601 format. FMT can be 'date' (default), 'hours', 'minutes', 'seconds', or 'ns'. e.g.: 2006-08-14T02:34:56-06:00
-R, --rfc-email            Output date and time in RFC 5322 format. e.g.: Mon, 14 Aug 2006 02:34:56 -0600
--rfc-3339=FMT             Output date/time in RFC 3339 format. FMT can be 'date', 'seconds', or 'ns'. e.g.: 2006-08-14 02:34:56-06:00
-r, --reference=FILE       Display the last modification time of FILE.
-s, --set=STRING           Set time described by STRING.
-u, --utc, --universal     Print or set Coordinated Universal Time (UTC).
--help                     Display help and exit.
--version                  Output version information and exit.
```

## Return Value

Returns 0 on success, and a non-zero value if an invalid option or parameter is provided.

## Examples

```shell
# Format output:
date +"%Y-%m-%d"
2009-12-07

# Yesterday's date:
date -d "1 day ago" +"%Y-%m-%d"
2012-11-19

# Time after 2 seconds:
date -d "2 second" +"%Y-%m-%d %H:%M.%S"
2012-11-20 14:21.31

# The legendary 1234567890 seconds:
date -d "1970-01-01 1234567890 seconds" +"%Y-%m-%d %H:%M:%S"
# Or
date -d@1234567890 +"%F %T"
# Result
2009-02-13 23:02:30

# Time format conversion:
date -d "2009-12-12" +"%Y/%m/%d %H:%M.%S"
# Result
2009/12/12 00:00.00

# Apache format conversion:
date -d "Dec 5, 2009 12:00:37 AM" +"%Y-%m-%d %H:%M.%S"
# Result
2009-12-05 00:00.37

# Time offset with conversion:
date -d "Dec 5, 2009 12:00:37 AM 2 year ago" +"%Y-%m-%d %H:%M.%S"
# Result
2007-12-05 00:00.37

# Time addition and subtraction:
date +%Y%m%d                   # Show year, month, day
date -d "+1 day" +%Y%m%d       # Show tomorrow's date
date -d "-1 day" +%Y%m%d       # Show yesterday's date
date -d "-1 month" +%Y%m%d     # Show last month's date
date -d "+1 month" +%Y%m%d     # Show next month's date
date -d "-1 year" +%Y%m%d      # Show last year's date
date -d "+1 year" +%Y%m%d      # Show next year's date

# Setting time:
date -s                         # Set current time (requires root)
date -s 20120523                # Set date to 20120523, time resets to 00:00:00
date -s 01:01:01                # Set specific time without changing date
date -s "01:01:01 2012-05-23"   # Set date and time
date -s "01:01:01 20120523"     # Set date and time
date -s "2012-05-23 01:01:01"   # Set date and time
date -s "20120523 01:01:01"     # Set date and time

# Measuring command execution time:
start=$(date +%s)
nmap example.com &> /dev/null
end=$(date +%s)
difference=$(( end - start ))
echo $difference seconds.

# Output string with time (e.g., Current time: 2019/05/19):
# Common method:
echo "Current time: $(date +"%Y/%m/%d")"
# Alternative method:
suffix='Current time:'
date +"${suffix} %Y/%m/%d"
```

### Note

1. This command is part of the `GNU coreutils` package. For more information, see `man -s 1 date` or `info coreutils 'date invocation'`.
