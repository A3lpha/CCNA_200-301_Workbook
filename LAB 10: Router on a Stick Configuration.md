# Router on a Stick
Today router software makes it possible to configure one router interface as multiple trunks by using sub-interfaces. In Figure, the physical GigabitEthernet 0/0 interface is logically subdivided into two logical interfaces. The one switch trunk is configured to trunk both VLAN 10 and VLAN 30, and each sub-interface on the router is assigned a separate VLAN. The router performs inter-VLAN routing by accepting VLAN-tagged traffic on the trunk interface coming from the adjacent switch. The router then forwards the routed traffic, VLAN-tagged for the destination VLAN, out the same physical interface that it used to receive the traffic.
LAB 10: Router on a Stick Configuration
# LAB OBJECTIVE AND ACTIVITIES:
This lab was written for Eve-ng Community, Pre-configured Lab can be downloaded from Course Page. The lab can also easily be completed using your own equipment or GNS3. Instructions. Open the accompanying Eve-ng Lab titled “Router on a Stick Configuration Lab”.  Follow the exercises below to complete this lab.
### Lab Purpose:
When configuring inter-VLAN routing using the router on a stick model, the physical interface of the router must be connected to a trunk link on the adjacent switch. On the router, subinterfaces are created for each unique VLAN on the network.
Each subinterface is assigned an IP address specific to its subnet/VLAN and is also configured to tag frames for that VLAN.
This way, the router can keep the traffic from each subinterface separated as it traverses the trunk link back to the switch.
## Switch
~~~
switch (config)# vlan 10
switch (config)# vlan 30
switch # configure terminalswitch (config)# interface vlan 10
switch (config-if)# ip address 172.17.10.2 255.255.255.0
switch (config-if)# interface vlan 30
switch (config-if)# ip address 172.17.30.2 255.255.255.0
switch (config-if)# interface GigabitEthernet 0/1
switch (config-if)# switchport mode access
switch (config-if)# switchport access vlan 30
switch (config-if)# interface GigabitEthernet 0/2
switch (config-if)# switchport mode access
switch (config-if)# switchport access vlan 10
switch (config-if)# end Switch(config)#  interface GigabitEthernet 0/0
Switch(config-line)# switchport trunk encapsulation dot1q
Switch(config-line)#  switchport mode trunk
Switch(config-line)# exit
~~~
## HQ Router configuration
~~~
HQ (config)# interface GigabitEthernet 0/0
HQ (config-if)# no shutdown
HQ (config-if)# interface GigabitEthernet 0/0.10
HQ (config-subif)# encapsulation dot1q 10
HQ (config-subif)# ip address 172.17.10.1 255.255.255.0
HQ (config-subif)# interface GigabitEthernet 0/0.30
HQ (config-subif)# encapsulation dot1q 30
HQ (config-subif)# ip address 172.17.30.1 255.255.255.0  
Configure IP Address for the PCs
PC-A: Ip 172.17.10.10 255.255.255.0 172.17.10.2
PC-B: Ip 172.17.30.10 255.255.255.0 172.17.30.2
~~~

# Congratulations! You have completed this lab.

