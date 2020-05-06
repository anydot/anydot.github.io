+++
date = "2013-05-30T18:10:00+01:00"
title = "How to install OpenSSH server on windows"

+++

1. `ccygwin openssh`
2. `ssh-host-config -y; cygrunsrv -S sshd` as Admin
        * When asked for value of CYGWIN value, enter: tty ntsec
        * This will create cyg_server local account if it isn't available yet
3. `ssh-user-config`
3. `netsh advfirewall firewall add rule name="OpenSSH" dir=in action=allow protocol=TCP localport=22` to allow incomming SSH connections
