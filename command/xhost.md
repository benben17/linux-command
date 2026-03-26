xhost
===

Control which X clients can connect to the X server

## Description

The **xhost command** is an access control tool for the X server, used to control which X clients are allowed to display their windows on the server. This command must be run from a machine that has a display connection. You can remove a hostname from the access list using the `-host` parameter. Be careful not to remove the current hostname; if you do, log out before making further changes.

### Syntax

```shell
xhost [+|-] [hostname]
```

### Parameters

*   `+`: Disable access control, allowing any host to connect to the local X server.
*   `-`: Enable access control, restricting access to only those hosts in the authorization list.
*   `hostname`: Specify the name of the host to be added to or removed from the list.

Running `xhost` without any arguments displays the current access control status and a list of authorized hosts.

For security reasons, options affecting access control should only be run from the controlling host (usually the server machine or login host).

To enable remote access by default, you can define hostnames in the `/etc/X?.hosts` files, where `?` represents the display number (e.g., `/etc/X0.hosts` for display `:0`).

**Caution:** If you remove the current machine from the access list, new connections (including attempts to add it back) will be refused. The only way to re-enable local connections would be to reset the X server, which would also terminate all existing connections.
