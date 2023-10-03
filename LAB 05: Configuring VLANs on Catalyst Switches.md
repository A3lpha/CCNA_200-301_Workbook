# LAB 05: Configuring VLANs on Catalyst Switches
LAB OBJECTIVE AND ACTIVITIES:
This lab was written for Eve-ng Community, Pre-configured Lab can be downloaded from Course Page. The lab can also easily be completed using your own equipment or GNS3. Instructions
Open the accompanying Eve-ng Lab titled “Configuring VLANs on Catalyst Switches”.
Follow the exercises below to complete this lab.
Lab Purpose:
VLAN configuration is a fundamental skill. VLANs allow you to segment your network into multiple, smaller broadcast domains. As a Cisco engineer, as well as in the Cisco CCNA exam, you will be expected to know how to configure VLANs on Cisco switches.
Lab Topology:
Please use the following topology to complete this lab exercise:
# Task 1:
~~~
In preparation for VLAN configuration, configure a hostname on Sw1 as well as the VLANs depicted in the topology.
~~~
# Task 2:
~~~
Configure ports GigabitEthernet 0/1 to GigabitEthernet 0/3 as access ports and assign them to the VLANs specified.
~~~
# Task 3:
Verify your VLAN configuration using relevant show commands in Cisco IOS.
Configuration and Verification
# Task 1:
~~~
Switch#configure terminal
Switch(config)#hostname SW1
Sw1(config)#vlan 10
Sw1(config-vlan)#name SALES
Sw1(config-vlan)#exit
Sw1(config)#vlan 20
Sw1(config-vlan)#name MANAGERS
Sw1(config-vlan)#exit
Sw1(config)#vlan 30
Sw1(config-vlan)#name ENGINEERS
Sw1(config-vlan)#exit
~~~  
NOTE: By default, Cisco switches are VTP servers so no configuration is necessary for server mode. Use the show vtp status command to look at the current VTP operating mode of the switch.

# Task 2:
~~~
Sw1(config)#interface GigabitEthernet0/1
Sw1(config-if)#switchport mode access
Sw1(config-if)#switchport access vlan 10
Sw1(config-if)#exit Sw1(config)#interface GigabitEthernet0/2
Sw1(config-if)#switchport mode access
Sw1(config-if)#switchport access vlan 20 Sw1(config-if)#exit
Sw1(config)#interface GigabitEthernet0/3
Sw1(config-if)#switchport mode access
Sw1(config-if)#switchport access vlan 30
Sw1(config-if)#exit  
Task 3:
Sw1#show vlan brief
~~~
Changing the Native VLAN and Shutting Down Unused Ports
Set any interface to trunk and then specify VLAN20 as the native VLAN for the trunk link.
~~~
Sw1# configure terminal
Sw1(config)# vlan 99
Sw1(config-vlan)# name Native VLAN
Sw1(config)#interface GigabitEthernet 0/0
Sw1(config-if)# switchport trunk encapsulation dot1q
Sw1(config-if)# switchport mode trunk
Sw1(config-if)# switchport trunk native vlan 99
Sw1#show ip interface brief
Sw1(config)#interface range GigabitEthernet 1/0 - 3
Sw1(config-if-range)# shutdown
~~~
Congratulations! You have completed this lab.

