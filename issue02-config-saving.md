# "copy running-config startup-config" not working
- After I executed "copy running-config startup-config, there is no configuration saved.

  ```
  switch# show running-config
  Current configuration:
  !
  !
  !
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
- If I do it with x86-64 docker image of the save version 0.2.1, it works as expected

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
  
