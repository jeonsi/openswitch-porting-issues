https://tree.taiga.io/project/openswitch/issue/676

# SFP+ module on some port is not recognized and it is alwasy admin-down even if configured with "no shutdown".
- If I insert an SFP+ into port 10 and 34, the SFP+ module is not recognized.
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
switch# show int 10 transceiver
Interface 10:
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

# Workaround
- Do not use port 10 and 34.

# Solution
- root cause: /etc/openswitch/platform/Accton/AS5712-54X/ports.yaml bug
- source repository: ops-hw-config
- https://github.com/open-switch/ops-hw-config/blob/master/Accton/AS5712-54X/ports.yaml
- commit: https://github.com/open-switch/ops-hw-config/commit/2674a53198a92f89f8ec04f99e1dd6858463eebe
