nfsstat
===

Display NFS (Network File System) statistics

## Description

The **nfsstat command** displays statistics about NFS (Network File System) and RPC (Remote Procedure Call) activity for both the client and the server.

### Syntax

```shell
nfsstat [options]
```

### Options

```shell
-s: Display statistics for the NFS server side only.
-c: Display statistics for the NFS client side only.
-n: Display NFS statistics only (default is both NFS and RPC).
-2: Display statistics for NFS version 2 only.
-3: Display statistics for NFS version 3 only.
-4: Display statistics for NFS version 4 only.
-m: Print information about each mounted NFS file system.
-r: Display RPC statistics only.
```

### Examples

To display information about the number of RPC and NFS calls sent and rejected by the client:

```shell
nfsstat -c
```

To display information specifically related to client NFS calls:

```shell
nfsstat -cn
```

To display RPC call information for both the client and the server:

```shell
nfsstat -r
```

To display information about the number of RPC and NFS calls received and rejected by the server:

```shell
nfsstat -s
```
