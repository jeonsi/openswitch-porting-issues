# [FAILED] Failed to start OpenSwitch stpd Module Daemon.
- When I boot the switch, it shows me **ops-stpd** related error.
```
root@switch:~# systemctl -l status ops-stpd
● ops-stpd.service - OpenSwitch stpd Module Daemon
   Loaded: loaded (/lib/systemd/system/ops-stpd.service; enabled; vendor preset: enabled)
   Active: failed (Result: exit-code) since Tue 2016-03-15 05:30:24 UTC; 6h ago
  Process: 338 ExecStart=/sbin/ip netns exec swns /usr/bin/ops-stpd --detach --pidfile -vSYSLOG:INFO (code=exited, status=1/FAILURE)
  Process: 287 ExecStartPre=/bin/rm -f /var/run/openvswitch/ops-stpd.pid (code=exited, status=0/SUCCESS)

Mar 15 05:30:24 ops-as5712 systemd[1]: Starting OpenSwitch stpd Module Daemon...
Mar 15 05:30:24 ops-as5712 systemd[1]: ops-stpd.service: control process exited, code=exited status=1
Mar 15 05:30:24 ops-as5712 systemd[1]: Failed to start OpenSwitch stpd Module Daemon.
Mar 15 05:30:24 ops-as5712 systemd[1]: Unit ops-stpd.service entered failed state.
Mar 15 05:30:24 ops-as5712 systemd[1]: ops-stpd.service failed.
Mar 15 05:30:24 ops-as5712 ip[338]: exec of "/usr/bin/ops-stpd" failed: No such file or directory
```
- There is no such file actually: /usr/bin/ops-stpd
```
root@switch:~# ls -l /usr/bin/ops-stpd
ls: cannot access /usr/bin/ops-stpd: No such file or directory
```

# Analysis
- stpd is in developing stage.
- In version 0.2.1, there is no ops-stpd.service file in /etc/systemd/system/multi-user.target.wants/
- In version 0.3.0, there is ops-stpd.service file in /etc/systemd/system/multi-user.target.wants/, but there is no ops-stpd packaged because it is in developing stage!

# Disable ops-stpd service until it actually works
- https://github.com/open-switch/ops-build/commit/315e622fec87a3b3d12ba6843183419996e399f2
