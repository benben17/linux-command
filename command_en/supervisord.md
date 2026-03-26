supervisord
===

A process control system for managing background services and persistent processes

## Installation

```shell
# Install supervisor
apt-get install supervisor
```

## Examples

Generate a configuration file `/etc/supervisord.conf`:

```shell
[program:app]
command=/usr/bin/gunicorn -w 1 wsgiapp:application
directory=/srv/www
user=www-data
```

`supervisord`: Start the supervisor service

```shell
supervisorctl start app
supervisorctl stop app
supervisorctl reload # Execute this after modifying/adding configuration files
```

## Download Links

https://pypi.python.org/pypi/meld3  
https://pypi.python.org/pypi/supervisor
