---
title: Scheduling
taxonomy:
    category: docs
---

Container Linux replaces cron with [systemd timers](https://coreos.com/os/docs/latest/scheduling-tasks-with-systemd-timers.html?target=_blank).  [Getting started with systemd](https://coreos.com/os/docs/latest/getting-started-with-systemd.html) contains examples of enabling, starting, and stopping containers.  [Docker container as a Linux system service](https://blog.marcnuri.com/docker-container-as-linux-system-service/) uses `docker start -a`/`docker stop` to start/stop containers.

## Example

```
[Unit]
Description=MySQL
After=docker.service
Wants=network-online.target docker.socket
Requires=docker.socket

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/docker start -a mysql
ExecStop=/usr/bin/docker stop mysql

[Install]
WantedBy=multi-user.target
```

* Create the file **mysql.service** in **/etc/systemd/system**
* Enable the service `systemctl enable mysql`
* Start the service `systemctl start mysql`
* Stop the service `systemctl stop mysql`

If the **mysql.service** file is changed, use `systemctl daemon-reload` to reflect the changes.


