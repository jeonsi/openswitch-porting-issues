# ARP resolution is delayed for 30 seconds

- https://tree.taiga.io/project/openswitch/issue/771

```
Before the problem:
=================
switch# show run interface 1
interface 1
   no shutdown
   ip address 192.168.10.101/24
   exit

switch# ping 192.168.10.1
PING 192.168.10.1 (192.168.10.1) 100(128) bytes of data.
108 bytes from 192.168.10.1: icmp_seq=1 ttl=255 time=0.459 ms

switch# show arp
ARP IPv4 Entries:
------------------
IPv4 Address     MAC                Port             State
192.168.10.1     a4:4c:11:6c:80:3f  1                reachable

Right after shutdown and no shutdown interface 1
================================
switch# conf t
switch(config)# int 1
switch(config-if)# shut
switch(config-if)# no shut
switch(config-if)# end
switch# show int 1

switch# ping 192.168.10.1
PING 192.168.10.1 (192.168.10.1) 100(128) bytes of data.
From 192.168.10.101 icmp_seq=1 Destination Host Unreachable
From 192.168.10.101 icmp_seq=2 Destination Host Unreachable
From 192.168.10.101 icmp_seq=3 Destination Host Unreachable
From 192.168.10.101 icmp_seq=4 Destination Host Unreachable

switch# show arp
ARP IPv4 Entries:
------------------
IPv4 Address     MAC                Port             State
192.168.10.1                        1                failed

switch# show int 1

Interface 1 is up
 Admin state is up

Waiting for 30 seconds, and after that
====================
switch# ping 192.168.10.1
PING 192.168.10.1 (192.168.10.1) 100(128) bytes of data.
108 bytes from 192.168.10.1: icmp_seq=1 ttl=255 time=0.869 ms

switch# show arp
ARP IPv4 Entries:
------------------
IPv4 Address     MAC                Port             State
192.168.10.1     a4:4c:11:6c:80:3f  1                reachable
```

# Solved
It's not the bug of OpenSwitch.
It the side effect of peering switch, which has stp portfast feature disabled.
The following configuration on peer switch will solve the problem.

```
spanning-tree portfast trunk
```
