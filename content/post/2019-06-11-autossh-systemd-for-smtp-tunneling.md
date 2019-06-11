---
title: "Using autossh, systemd and restirected ssh forwarding for tunneling SMTP"
date: 2019-06-11T13:25:58Z
draft: false
---

I didn't want to turn a full-blow MTA on my RaspberryPI and decided to give the Dragonfly MTA a try. Unfortunately my home DSL line IP block is properly marked as
a dial-up line and thus Google rejects all the emails I'm trying to send to myself :)

<!--more-->

```
root@raspberrypi:~# cat /etc/systemd/system/autossh-smtp.service
[Unit]
Description=AutoSSH target to run the SMTP forwarding to oratica
After=network.target

[Service]
Environment="AUTOSSH_GATETIME=0"
ExecStart=/usr/bin/autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -T -N -i /root/.ssh/id_ed25519_smtp_smarthost -p 30022 -L 25:127.0.0.1:25 prema@oratica.anydot.in

[Install]
WantedBy=multi-user.target
root@raspberrypi:~# systemctl daemon-reload
root@raspberrypi:~# systemctl start autossh-smtp.service
root@raspberrypi:~# systemctl enable autossh-smtp.service
Created symlink /etc/systemd/system/multi-user.target.wants/autossh-smtp.service → /etc/systemd/system/autossh-smtp.service.
```

```
Authorized keys
restrict,port-forwarding,permitopen="127.0.0.1:25",command="/bin/true" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJmSOrHQJ8JBumzj7Psyl3pThu6KQBdJhiLps0uvZgTa root@raspberrypi
```


