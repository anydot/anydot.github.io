---
title: "Shrinking WSL2 volume"
date: 2020-05-06T10:41:18+02:00
---

As WSL2 uses EXT4 in VHD volume, the VHDs size can grow in time as one uses the WSL. Deleting files isn't enough and one has to zero-out the free blocks and run the VHD compaction.

From WSL2 console:
``` bash
mount /dev/sdb -o remount,ro
zerofree -v /dev/sdb
```

From the Windows host's Admin powershell:
``` posh
# Install the HyperV management and powershell optional features
wsl --shutdown
Import-Module -Name Hyper-v
Optimize-VHD -Mode Full -Verbose $env:LOCALAPPDATA\Packages\$((Get-AppxPackage *Ubuntu*).PackageFamilyName)\LocalState\ext4.vhdx
```



