cal
===

Displays a calendar of the current month or a specified date.

## Description

The **cal command** is used to display the calendar for the current month or a specified date. If no parameters are provided, it displays the current month.

A single parameter specifies the year to be displayed (1 - 9999); note that the year must be fully specified: `cal 89` will not display the calendar for 1989. Two parameters represent the month (1 - 12) and the year. If no parameters are specified, the calendar for the current month is displayed.

A year starts on January 1st.

The Gregorian Reformation is considered to have occurred on September 3, 1752. Prior to this, most countries had already accepted the reform (though some did not until the early 20th century). Ten days were omitted following that date, so the calendar for that month is somewhat unusual.

### Syntax

```shell
cal [ -mjy ] [ month ] [ year ]
```

### Options

```shell
-l # Display single-month output.
-3 # Display the previous, current, and next month's calendars.
-s # Display Sunday as the first day of the week.
-m # Display Monday as the first day of the week (default is Sunday).
-j # Display Julian dates (day of the year starting from January 1st as 1).
-y # Display a calendar for the current year.
```

### Parameters

```shell
month: Specify the month.
year: Specify the year.
```

### Examples

Executing the `cal` command alone prints the calendar for the current month:

```shell
[root@localhost ~]# cal
   December 2013     
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
```

```shell
[root@localhost ~]# cal -j
        December 2013        
  Su   Mo   Tu   We   Th   Fr   Sa
335 336 337 338 339 340 341
342 343 344 345 346 347 348
349 350 351 352 353 354 355
356 357 358 359 360 361 362
363 364 365
```

```shell
[root@localhost ~]# cal -3

    September 2021          October 2021          November 2021
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
          1  2  3  4                  1  2      1  2  3  4  5  6
 5  6  7  8  9 10 11   3  4  5  6  7  8  9   7  8  9 10 11 12 13
12 13 14 15 16 17 18  10 11 12 13 14 15 16  14 15 16 17 18 19 20
19 20 21 22 23 24 25  17 18 19 20 21 22 23  21 22 23 24 25 26 27
26 27 28 29 30        24 25 26 27 28 29 30  28 29 30
                      31
```
