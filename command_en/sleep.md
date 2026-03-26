sleep
===

Delay for a specified amount of time.

## Description

The **sleep command** pauses the execution for a specified duration.

### Syntax

```shell
sleep(parameter)
```

### Parameters

Time: Specifies the length of time to pause, including:

* `2s`: 2 seconds
* `2m`: 2 minutes
* `2h`: 2 hours
* `2d`: 2 days
* `infinity`: Permanently

### Example

When writing monitoring scripts that run in a loop, setting a time interval is essential. Below is a demonstration of a Shell progress bar script that generates delays.

```shell
#!/bin/bash

b=''
for ((i=0;$i<=100;i++))
 do
 printf "Progress:[%-100s]%d%%\r" $b $i
 sleep 0.1
 b=#$b
 done
echo
```
