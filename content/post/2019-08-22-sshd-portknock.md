---
title: "2019 08 22 Sshd Portknock"
date: 2019-08-22T12:07:39Z
draft: true
---

```
[options]
UseSyslog

[openSSH]
sequence    = 60030,60035,60040
seq_timeout = 5
command     = /sbin/ipset add sshd -exist %IP%
tcpflags    = syn
```

```
-A INPUT -p tcp -m multiport --dports 22 -j f2b-sshd
-A INPUT -s 10.0.0.0/8 -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 22 -m set --match-set sshd src -j ACCEPT
-A INPUT -p tcp -m tcp --dport 22 -j DROP
```

```
iptables-persistent ipset-persistent
```


