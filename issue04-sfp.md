# SFP+ module on some port is not recognized
- If I insert an SFP+ into port 9 and 34, the SFP+ module is not recognized.
- normal case
```
switch# show int 1 transceiver
Interface 1:
 Connector: SFP+
 Transceiver module: SFP_SR
 Connector status: supported
 Vendor name: Edgecore
 Part number: ET5402-SR
 Part revision:
 Serial number: F151550055
 Supported speeds: 10000
```
- abnormal case
```
switch# show int 9 transceiver
Interface 9:
 Connector: SFP+
 Transceiver module: not present

switch# show int 34 transceiver
Interface 34:
 Connector: SFP+
 Transceiver module: not present
```
- I don't think the SFP+ module problematic. The same SFP+ module is recognized when inserted in the other ports.
- I don't think the port itself is problematic, either. Because when I was using Cumulus, I've never experienced such problems.
  For the exact probe, I should install Cumulus again, but it's very time consuming.