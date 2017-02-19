+++
date = "2013-06-21T18:10:00+01:00"
title = "Setting up VirtualBox for NAT DNS"

+++

Sometimes it can be useful to use host for resolving instead of guest directly contacting DNS network in the current network; in case you are changing DNS servers a lot (imagine notebook and changing networks) 
or in cases where there's VPN tunnel involved with split-routing; it can be useful to use host for resolving instead of guest directly contacting DNS network in the current network.
Note this only works if you use NAT type of network in Virtualbox.

1. Shutdown given guest
2. `````$ VBoxManage modifyvm "Virtual machine name" --natdnsproxy1 on --natdnshostresolver1 on`````
3. Profit
