# I want to connect the OpenSwitch port with Cisco C4948 via 1 Gbps optic, but I can't figure out the right configuration
- This is the OpenSwitch side configuration
```
interface 4
    no shutdown
    speed 1000
```
- This is the C4948 side configuration
```
interface GigabitEthernet1/45
 switchport trunk encapsulation dot1q
 switchport mode trunk
 speed nonegotiate
```
```
switch# show interface 4

Interface 4 is down
 Admin state is up
 Hardware: Ethernet, MAC Address: 70:72:cf:fd:e1:ec
 MTU 1500
 Half-duplex
 Speed 0 Mb/s
 Auto-Negotiation is turned on
 Input flow-control is off, output flow-control is off
 RX
            0 input packets              0 bytes
            0 input error                0 dropped
            0 CRC/FCS
 TX
            0 output packets             0 bytes
            0 input error                8 dropped
            0 collision

% Command incomplete.
switch#
```
