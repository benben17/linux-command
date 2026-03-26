domainname
===

Display or set the system's NIS/YP domain name.

## Description

The **domainname** command is used to display and set the NIS (Network Information Service) domain name of the system.

### Syntax

```shell
domainname (options) (parameters)
```

### Options

```shell
-v    Verbose mode.
-F    Read the domain name from a specified file.
```

### Parameters

NIS Domain Name: Specifies the NIS domain name to be set.

### Examples

```shell
[root@AY1307311912260196fcZ ~]# domainname -v
getdomainname()=`(none)'
(none)
 [root@AY1307311912260196fcZ ~]# domainname
www.jsdig.com

[root@AY1307311912260196fcZ ~]# domainname -v
getdomainname()=`www.jsdig.com'
www.jsdig.com
```
