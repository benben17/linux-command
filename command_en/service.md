service
===

Utility for controlling system services.

## Description

The **service command** is a utility used in Red Hat Linux and compatible distributions to control system services. It can start, stop, restart, and shut down system services, as well as display the current status of all system services.

### Syntax

```shell
service(options)(parameters)
```

### Options

```shell
-h: Display help information.
--status-all: Display the status of all services.
```

### Parameters

*   Service name: The name of the service to be controlled, i.e., the filename of the script in the `/etc/init.d` directory.
*   Control command: The control command supported by the system service script.

### Examples

When modification of information such as the hostname or IP address is made, it is often necessary to restart the network for changes to take effect.

```shell
service network status
Configured devices:
lo eth0
Currently active devices:
lo eth0

service network restart
Shutting down interface eth0:                                 [  OK  ]
Shutting down loopback interface:                             [  OK  ]
Setting network parameters:                                   [  OK  ]
Bringing up loopback interface:                               [  OK  ]
Bringing up interface eth0:                                   [  OK  ]
```

Restart MySQL:

```shell
service mysqld status
mysqld (pid 1638) is running...

service mysqld restart
Stopping MySQL:                                               [  OK  ]
Starting MySQL:                                               [  OK  ]
```
