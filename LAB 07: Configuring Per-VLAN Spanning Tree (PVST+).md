# LAB 07: Configuring Per-VLAN Spanning Tree (PVST+)
## LAB OBJECTIVE AND ACTIVITIES:
This lab was written for Eve-ng Community, Pre-configured Lab can be downloaded from Course Page. The lab can also easily be completed using your own equipment or GNS3. Instructions. Open the accompanying Eve-ng Lab titled “Configuring Per-VLAN Spanning Tree (PVST+)”.  
Follow the exercises below to complete this lab.
Lab Objectives
The network topology for the configuration of PVST+ using commands covered in this chapter. Assume that other commands needed for connectivity have already been configured.
# Core Switch:
~~~
Switch> enable 
Switch# configure terminal 
Switch(config)# hostname Core 
Core(config)# no ip domain-lookup 
Core(config)# vtp mode server 
Core(config)# vtp domain Hurbad 
Core(config)# interface range gigabitEthernet 0/1 – 2
Core(config-if-range)# switchport trunk encapsulation dot1q
Core(config-if-range)# switchport mode trunk
Core(config-if-range)# exit 
Core(config)# VLAN 10
Core(config)# name Accounting
Core(config)# exit
Core(config)# VLAN 20
Core(config)# name Marketing
Core(config)# exit
Core(config)# spanning-tree vlan 1 root primary
Core(config)# exit
~~~
Distribution 1 Switch:
~~~
Switch> enable
Switch# configure terminal
Switch(config)# hostname DSW1
DSW1(config)# no ip domain-lookup
DSW1(config)# vtp domain Hurbad
DSW1(config)# vtp mode client
DSW1(config)# interface range gigabitEthernet 0/0 - 2
DSW1(config-if-range)# switchport trunk encapsulation dot1q
DSW1(config-if-range)# switchport mode trunk
DSW1(config-if-range)# exit 
DSW1(config)# interface range gigabitEthernet 1/0 - 1
DSW1(config-if-range)# switchport trunk encapsulation dot1q
DSW1(config-if-range)# switchport mode trunk
DSW1(config-if-range)# exit
DSW1(config)# interface range ethernet 1/0 – 1
DSW1(config-if-range)# switchport trunk encapsulation dot1q
DSW1(config-if-range)# switchport mode trunk
DSW1(config-if-range)# exit
DSW1(config)# spanning-tree vlan 10 root primary
DSW1(config)# exit
~~~
# Distribution 2 Switch:
~~~
Switch> enable
Switch# configure terminal
Switch(config)# hostname DSW2
DSW2(config)# no ip domain-lookup
DSW2(config)# vtp domain Hurbad
DSW2(config)# vtp mode client
DSW2(config)# interface range gigabitEthernet 0/0 – 3
DSW2(config-if-range)# switchport trunk encapsulation dot1q
DSW2(config-if-range)# switchport mode trunk
DSW2(config-if-range)# exit
DSW2(config)# spanning-tree vlan 20 root primary
DSW2(config)# exit
~~~
Access 1 Switch:
~~~
Switch> enable
Switch# configure terminal
Switch(config)# hostname Access1
Access1 (config)# no ip domain-lookup
Access1 (config)# vtp domain Hurbad
Access1 (config)# vtp mode client
Access1(config)# interface range gigabitEthernet 0/0 - 2
Access1(config-if-range)# switchport trunk encapsulation dot1q
Access1(config-if-range)# switchport mode trunk
Access1(config-if-range)# exit
Access1(config)# interface gigabitEthernet 0/3
Access1(config-if-range)# switchport trunk encapsulation dot1q
Access1(config-if-range)# switchport mode trunk
Access1(config-if-range)# exit
~~~
# Access 2 Switch:
~~~
Switch> enable
Switch# configure terminal
Switch(config)# hostname Access2
Access2(config)# no ip domain-lookup
Access2(config)# vtp domain Hurbad
Access2(config)# vtp mode client
Access2(config)# interface range gigabitEthernet 0/0 - 3
Access2(config-if-range)# switchport trunk encapsulation dot1q
Access2(config-if-range)# switchport mode trunk
Access2(config-if-range)# exit
Access2(config)# interface range gigabitEthernet 1/0 - 1
Access2(config-if-range)# switchport trunk encapsulation dot1q
Access2(config-if-range)# switchport mode trunk
Access2(config-if-range)# exit
Access2(config)# interface gigabitEthernet 1/2
Access2(config-if-range)# switchport mode access
Access2(config-if-range)# spanning-tree portfast
Access2(config-if-range)# spanning-tree bpduguard enable
Access2 (config-if-range)# exit
Access2(config)# spanning-tree vlan 1,10,20 priority 61440
(Ensures this switch does not become the root switch for VLAN 10)
~~~
![](image)
## Troubleshooting Spanning Tree
 
# Congratulations! You have completed this lab.

