showmount
===

Display information about the NFS server's mount points.

## Description

The **showmount command** queries the "mountd" daemon to display information about the NFS server's mount points.

### Syntax

```shell
showmount [option] [parameter]
```

### Options

```shell
-d: List only the directories that have been mounted by some NFS client;
-e: Show the NFS server's export list.
```

### Parameters

NFS server: Specify the IP address or hostname of the NFS server.
