---
title: Scheduler
taxonomy:
    category: docs
---

[Scheduling tasks with systemd timers](https://coreos.com/os/docs/latest/scheduling-tasks-with-systemd-timers.html) contains an example configuration for scheduling in CoreOS.  See [systemd.timer — Timer unit configuration](https://www.freedesktop.org/software/systemd/man/systemd.timer.html) for more information on timers.  See [systemd.time — Time and date specifications](https://www.freedesktop.org/software/systemd/man/systemd.time.html#) for time and date specifications.

* Create a service in `/etc/systemd/system`
* Create a timer unit with the same name and a `.timer` suffix in `/etc/systemd/system`
* Check the status of a timer using `systemctl status xxx.timer`
* Enable timer using `systemctl start xxx.timer`
* List timers using `systemctl list-timers`

## Example

### Service

/etc/systemd/system/update_cert.service

```
[Unit]
Description=Renew Let's Encrypt Certificate

[Service]
Type=oneshot
ExecStart=/bin/bash -c "/home/core/scripts/update_cert"
```

### Timer

/etc/systemd/system/update_cert.timer

```
[Unit]
Description=Update Let's Encrypt Certificate every 3 months

[Timer]
OnCalendar=*-02,05,08,11-01 00:00:00 America/New_York
```
