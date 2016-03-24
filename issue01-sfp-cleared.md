# SFP+ module on some port is not recognized
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
switch# show interface 10 tr

Interface 10:
 Connector: SFP+
 Transceiver module: not present

switch# show int 34 transceiver
Interface 34:
 Connector: SFP+
 Transceiver module: not present
```
- I don't think the SFP+ module problematic. The same SFP+ module is recognized when inserted in the other ports.

# Solution
```
openswitch 아래 이슈와 관련하여 원인파악이 되었고 조만간 source code가 수정될 것 같습니다.

이슈: https://github.com/jeonsi/openswitch-porting-issues/blob/master/issue01-sfp.md
원인: /etc/openswitch/platform/Accton/AS5712-54X/ports.yaml 파일 버그
조치: edge-core에서 수정된 파일을 hp로 전달 완료. 조만간 openswitch git에 반영 예상됨

참고)
해당 파일 source repository: ops-hw-config
https://github.com/open-switch/ops-hw-config/blob/master/Accton/AS5712-54X/ports.yaml

정확히 어느 line인지 확인하고 좀 더 빨리 시험해 보기 위해 아래 edge-core 개발자에게 해당 파일을 저에게도 좀 보내달라고 요청 해 놓은 상태입니다.
```
- https://github.com/open-switch/ops-hw-config/commit/2674a53198a92f89f8ec04f99e1dd6858463eebe
