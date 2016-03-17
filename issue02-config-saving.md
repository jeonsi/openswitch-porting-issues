# "copy running-config startup-config" not working
- After I executed "copy running-config startup-config, there is no configuration saved.

  ```
  switch# conf t
  switch(config)# interface mgmt
  switch(config-if-mgmt)# ip static 10.10.10.2/24
  switch(config-if-mgmt)# default-gateway 10.10.10.1
  switch(config-if-mgmt)# end
  switch# show running-config
  Current configuration:
  !
  !
  !
  interface mgmt
      ip static 10.10.10.2/24
      default-gateway 10.10.10.1
  switch# show startup-config
  No saved configuration exists
  switch# copy running-config startup-config
  switch# show startup-config
  Startup configuration:
  !
  switch# show running-config
  Current configuration:
  !
  !
  !
  interface mgmt
      ip static 10.10.10.2/24
      default-gateway 10.10.10.1
  switch# copy running-config startup-config
  switch# show startup-config
  Startup configuration:
  !
  switch# show startup-config
  Startup configuration:
  !
  switch#
  switch#
  switch#
  switch# show startup-config
  Startup configuration:
  !
  switch#
  ```
- If I do it with x86-64 docker image of the same version 0.2.1, it works as expected

  ```
  switch# conf t
  switch(config)# int mgmt
  switch(config-if-mgmt)# ip static 10.10.10.2/24
  switch(config-if-mgmt)# default-gateway 10.10.10.1
  switch(config-if-mgmt)# end
  switch# show run
  Current configuration:
  !
  !
  !
  interface mgmt
      ip static 10.10.10.2/24
      default-gateway 10.10.10.1
  switch# copy running-config startup-config
  switch# show startup-config
  Startup configuration:
  !
  !
  !
  interface mgmt
      ip static 10.10.10.2/24
      default-gateway 10.10.10.1
  switch#
  ```
  
# Analysis
- If I check with "show startup-config json", something shows:
```
switch# show startup-config
Startup configuration:
!
switch#
```
```
switch# sh startup-config json
Startup configuration:
{
    "Interface": {
        "1": {
            "name": "1",
            "type": "system",
            "user_config": {
                "admin": "up"
            }
        },
        "10": {
            "name": "10",
            "type": "system"
        },
        "11": {
            "name": "11",
            "type": "system"
        },
        "12": {
            "name": "12",
            "type": "system"
        },
        "13": {
            "name": "13",
            "type": "system"
        },
        "14": {
            "name": "14",
            "type": "system"
        },
        "15": {
            "name": "15",
            "type": "system"
        },
        "16": {
            "name": "16",
            "type": "system"
        },
        "17": {
            "name": "17",
            "type": "system"
        },
        "18": {
            "name": "18",
            "type": "system"
        },
        "19": {
            "name": "19",
            "type": "system"
        },
        "2": {
            "name": "2",
            "type": "system",
            "user_config": {
                "admin": "up"
            }
        },
        "20": {
            "name": "20",
            "type": "system"
        },
        "21": {
            "name": "21",
            "type": "system"
        },
        "22": {
            "name": "22",
            "type": "system"
        },
        "23": {
            "name": "23",
            "type": "system"
        },
        "24": {
            "name": "24",
            "type": "system"
        },
        "25": {
            "name": "25",
            "type": "system"
        },
        "26": {
            "name": "26",
            "type": "system"
        },
        "27": {
            "name": "27",
            "type": "system"
        },
        "28": {
            "name": "28",
            "type": "system"
        },
        "29": {
            "name": "29",
            "type": "system"
        },
        "3": {
            "name": "3",
            "type": "system",
            "user_config": {
                "admin": "up"
            }
        },
        "30": {
            "name": "30",
            "type": "system"
        },
        "31": {
            "name": "31",
            "type": "system"
        },
        "32": {
            "name": "32",
            "type": "system"
        },
        "33": {
            "name": "33",
            "type": "system"
        },
        "34": {
            "name": "34",
            "type": "system"
        },
        "35": {
            "name": "35",
            "type": "system"
        },
        "36": {
            "name": "36",
            "type": "system"
        },
        "37": {
            "name": "37",
            "type": "system"
        },
        "38": {
            "name": "38",
            "type": "system"
        },
        "39": {
            "name": "39",
            "type": "system"
        },
        "4": {
            "name": "4",
            "type": "system"
        },
        "40": {
            "name": "40",
            "type": "system"
        },
        "41": {
            "name": "41",
            "type": "system"
        },
        "42": {
            "name": "42",
            "type": "system"
        },
        "43": {
            "name": "43",
            "type": "system"
        },
        "44": {
            "name": "44",
            "type": "system"
        },
        "45": {
            "name": "45",
            "type": "system"
        },
        "46": {
            "name": "46",
            "type": "system"
        },
        "47": {
            "name": "47",
            "type": "system"
        },
        "48": {
            "name": "48",
            "type": "system"
        },
        "49": {
            "name": "49",
            "split_children": [
                "49-3",
                "49-4",
                "49-2",
                "49-1"
            ],
            "type": "system"
        },
        "49-1": {
            "name": "49-1",
            "split_parent": [
                "49"
            ],
            "type": "system"
        },
        "49-2": {
            "name": "49-2",
            "split_parent": [
                "49"
            ],
            "type": "system"
        },
        "49-3": {
            "name": "49-3",
            "split_parent": [
                "49"
            ],
            "type": "system"
        },
        "49-4": {
            "name": "49-4",
            "split_parent": [
                "49"
            ],
            "type": "system"
        },
        "5": {
            "name": "5",
            "type": "system"
        },
        "50": {
            "name": "50",
            "split_children": [
                "50-2",
                "50-1",
                "50-4",
                "50-3"
            ],
            "type": "system"
        },
        "50-1": {
            "name": "50-1",
            "split_parent": [
                "50"
            ],
            "type": "system"
        },
        "50-2": {
            "name": "50-2",
            "split_parent": [
                "50"
            ],
            "type": "system"
        },
        "50-3": {
            "name": "50-3",
            "split_parent": [
                "50"
            ],
            "type": "system"
        },
        "50-4": {
            "name": "50-4",
            "split_parent": [
                "50"
            ],
            "type": "system"
        },
        "51": {
            "name": "51",
            "split_children": [
                "51-3",
                "51-4",
                "51-2",
                "51-1"
            ],
            "type": "system"
        },
        "51-1": {
            "name": "51-1",
            "split_parent": [
                "51"
            ],
            "type": "system"
        },
        "51-2": {
            "name": "51-2",
            "split_parent": [
                "51"
            ],
            "type": "system"
        },
        "51-3": {
            "name": "51-3",
            "split_parent": [
                "51"
            ],
            "type": "system"
        },
        "51-4": {
            "name": "51-4",
            "split_parent": [
                "51"
            ],
            "type": "system"
        },
        "52": {
            "name": "52",
            "split_children": [
                "52-2",
                "52-1",
                "52-4",
                "52-3"
            ],
            "type": "system"
        },
        "52-1": {
            "name": "52-1",
            "split_parent": [
                "52"
            ],
            "type": "system"
        },
        "52-2": {
            "name": "52-2",
            "split_parent": [
                "52"
            ],
            "type": "system"
        },
        "52-3": {
            "name": "52-3",
            "split_parent": [
                "52"
            ],
            "type": "system"
        },
        "52-4": {
            "name": "52-4",
            "split_parent": [
                "52"
            ],
            "type": "system"
        },
        "53": {
            "name": "53",
            "split_children": [
                "53-4",
                "53-1",
                "53-2",
                "53-3"
            ],
            "type": "system"
        },
        "53-1": {
            "name": "53-1",
            "split_parent": [
                "53"
            ],
            "type": "system"
        },
        "53-2": {
            "name": "53-2",
            "split_parent": [
                "53"
            ],
            "type": "system"
        },
        "53-3": {
            "name": "53-3",
            "split_parent": [
                "53"
            ],
            "type": "system"
        },
        "53-4": {
            "name": "53-4",
            "split_parent": [
                "53"
            ],
            "type": "system"
        },
        "54": {
            "name": "54",
            "split_children": [
                "54-4",
                "54-3",
                "54-1",
                "54-2"
            ],
            "type": "system"
        },
        "54-1": {
            "name": "54-1",
            "split_parent": [
                "54"
            ],
            "type": "system"
        },
        "54-2": {
            "name": "54-2",
            "split_parent": [
                "54"
            ],
            "type": "system"
        },
        "54-3": {
            "name": "54-3",
            "split_parent": [
                "54"
            ],
            "type": "system"
        },
        "54-4": {
            "name": "54-4",
            "split_parent": [
                "54"
            ],
            "type": "system"
        },
        "6": {
            "name": "6",
            "type": "system"
        },
        "7": {
            "name": "7",
            "type": "system"
        },
        "8": {
            "name": "8",
            "type": "system"
        },
        "9": {
            "name": "9",
            "type": "system"
        },
        "bridge_normal": {
            "name": "bridge_normal",
            "type": "internal",
            "user_config": {
                "admin": "up"
            }
        },
        "vlan200": {
            "name": "vlan200",
            "type": "internal",
            "user_config": {
                "admin": "up"
            }
        }
    },
    "Port": {
        "bridge_normal": {
            "interfaces": [
                "bridge_normal"
            ],
            "name": "bridge_normal"
        },
    },
    "System": {
        "aaa": {
            "fallback": "true",
            "radius": "false",
            "ssh_passkeyauthentication_enable": "true",
            "ssh_publickeyauthentication_enable": "true"
        },
        "asset_tag_number": "",
        "bridges": {
            "bridge_normal": {
                "datapath_type": "",
                "name": "bridge_normal",
                "ports": [
                    "bridge_normal",
                    "2"
                ],
                "vlans": {
                    "VLAN1024": {
                        "admin": [
                            "up"
                        ],
                        "id": 1024,
                        "name": "VLAN1024"
                    },
                    "VLAN1025": {
                        "admin": [
                            "up"
                        ],
                        "id": 1025,
                        "name": "VLAN1025"
                    }
                }
            }
        },
        "hostname": "",
        "mgmt_intf": {
            "default_gateway": "10.10.10.1",
            "ip": "10.10.10.2",
            "mode": "static",
            "name": "eth0",
            "subnet_mask": "24"
        },
        "vrfs": {
            "vrf_default":
                "name": "vrf_default",
                "ports": [
                ]
            }
        }
    }
}
switch#
```
- After rebooting the switch, I can't connect the swich remotely.
- from the console:
  - no running configuration
  - "show startup-config" gives strange errors.
  - "show startup-config json" gives the same contents before rebooting
```
ops-as5712# sh run
Current configuration:
!
!
!
ops-as5712# show startup-config
Startup configuration:
Traceback (most recent call last):
  File "/usr/bin/cfgdbutil", line 9, in <module>
    load_entry_point('ops-cfgd==1.0', 'console_scripts', 'cfgdbutil')()
  File "/usr/lib/python2.7/site-packages/cfgdbutil.py", line 258, in main
    if func(args) is False:
  File "/usr/lib/python2.7/site-packages/cfgdbutil.py", line 73, in show_config
    run_config_util.write_config_to_db(parsed)
  File "/usr/lib/python2.7/site-packages/runconfig/runconfig.py", line 48, in write_config_to_db
    self.idl, data)
  File "/usr/lib/python2.7/site-packages/runconfig/declarativeconfig.py", line 635, in write_config_to_db
    validator_adapter, errors)
  File "/usr/lib/python2.7/site-packages/runconfig/declarativeconfig.py", line 477, in setup_table
    schema, idl, validator_adapter, errors)
  File "/usr/lib/python2.7/site-packages/runconfig/declarativeconfig.py", line 344, in setup_row
    current_row)
  File "/usr/lib/python2.7/site-packages/runconfig/declarativeconfig.py", line 382, in setup_row
    errors)
  File "/usr/lib/python2.7/site-packages/runconfig/declarativeconfig.py", line 199, in setup_row
    idl.tables[table])
  File "/usr/lib/python2.7/site-packages/opsrest/utils/utils.py", line 521, in index_to_row
    elif str(row.__getattr__(index)) != value:
  File "/usr/lib/python2.7/site-packages/ovs/db/idl.py", line 553, in __getattr__
    (self.__class__.__name__, column_name))
AttributeError: Row instance has no attribute 'ip_address'
!
!
!
ops-as5712#
```
- If I try to configure, it's impossible:

```
ops-as5712# conf t
ops-as5712(config)# int mgmt
ops-as5712(config-if-mgmt)# ip static 10.10.10.2/24
% Command failed.
ops-as5712(config-if-mgmt)#
```
- I can't configure nothing!!!
- configuration is stored somewhere as json format file, but it is not actually get used.
- Configuration DB is corrupted, and make the system unconfigurable.
