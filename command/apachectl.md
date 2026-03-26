apachectl
===

A front-end control tool for the Apache HTTP server.


## Description

The **apachectl command** is a front-end control interface for the Apache Web server, used to start, stop, and restart the Web server process.

### Syntax

```
apachectl [parameters]
```

### Parameters

* configtest: Check the configuration file for syntax errors.
* fullstatus: Display full status information from the server.
* graceful: Restart the Apache server gracefully by sending a SIGUSR1 signal (does not terminate existing connections).
* help: Display help information.
* restart: Restart the Apache server.
* start: Start the Apache server.
* status: Display summary status information from the server.
* stop: Stop the Apache server.
