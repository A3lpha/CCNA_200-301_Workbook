# LAB 09: Configuring CDP and LLDP
## LAB OBJECTIVE AND ACTIVITIES:
The objective of this lab exercise is for you to learn and understand how to enable CDP and adjust CDP timers.
## Lab Purpose:
Understanding CDP and LLDP is a fundamental skill. CDP is a proprietary Cisco protocol that can be used for device discovery as well as internetwork troubleshooting. As a Cisco engineer, as well as in the Cisco CCNA exam, you will be expected to know how to enable and use CDP in internetwork discovery and troubleshooting.
## Lab Topology:
Please use the following topology to complete this lab:
# Task 1:
Configure hostnames on R1 and Sw1 as illustrated in the topology.
Task 2:
Configure an IP address of 172.29.100.1/24 on R1 GigabitEthernet 0/0.
# Task 3:
Configure VLAN200 on Sw1 and name it CDP_VLAN. Configure interface VLAN200 on Sw1 and assign it the IP address 172.29.100.2/24. Assign port GigabitEthernet 0/0 on Sw1 to this VLAN.
# Task 4:
Enable CDP on R1 and Sw1 globally (it’s already on by default but you can practice the command). Configure R1 and Sw1 to send CDP packets every 10 seconds. The timer command won’t work on Packet Tracer so use live equipment, GNS3, or Eve-NG.
# Task 5:
Use CDP to see detailed information about Sw1 from R1. Familiarize yourself with the information provided.
# Task 6:
Now disable CDP on the router interface and disable CDP globally on the switch.
CDP Configuration and Verification
# Task 1:
For reference information on configuring hostnames, please refer to earlier labs.
# Task 2:
~~~
R1# configure terminal 
Enter configuration commands, one per line. 
End with CTRL/Z. 
R1(config)# interface GigabitEthernet 0/0
R1(config-if)# ip address 172.29.100.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# end
Sw1# configure terminal 
Enter configuration commands, one per line.  
End with CTRL/Z.
Sw1(config)# vlan200
Sw1(config-vlan)# name CDP_VLAN
Sw1(config-vlan)# exit
Sw1(config)# interface vlan1
Sw1(config-if)# shutdown
Sw1(config-if)# exit
Sw1(config)# interface vlan 200
Sw1(config-if)# no shutdown
Sw1(config-if)# ip address 172.29.100.2 255.255.255.0
Sw1(config-if)# exit
Sw1(config)# interface GigabitEthernet 0/0
Sw1(config-if)# switchport mode access
Sw1(config-if)# switchport access vlan 200
Sw1(config-if)# end
Sw1# ping 172.29.100.1 
Type escape sequence to abort. 
Sending 5, 100-byte ICMP Echos to 172.29.100.1, timeout is 2 seconds:
!!!!! 
Success rate is 100 percent (5/5), 
round-trip min/avg/max = 1/203/1000 ms Sw1#
~~~
Task 3:
~~~
R1# configure terminal
Enter configuration commands, one per line. 
End with CTRL/Z. R1(config)#cdp run
R1(config)# cdp timer 10
R1(config)# end
R1#show cdp interface GigabitEthernet 0/0
GigabitEthernet 0/0 is up, line protocol is up Encapsulation ARPA Sending CDP packets every 10 seconds Holdtime is 180 seconds 
Sw1#configure terminal
Enter configuration commands, one per line. 
End with CTRL/Z.
Sw1(config)# cdp run
Sw1(config)# cdp timer 10
Sw1(config)# end
Sw1# show cdp interface GigabitEthernet 0/0
GigabitEthernet 0/0 is up, line protocol is up Encapsulation ARPA Sending CDP packets every 10 seconds Holdtime is 180 seconds
~~~
# Task 4:
~~~
R1# show cdp neighbors detail ------------------------- 
Device ID: Sw1 Entry address(es):   IP address: 172.29.100.2 Platform: cisco WS-C2950G-24-EI,  Capabilities: Switch IGMP Interface: GigabitEthernet 0/0,  Port ID (outgoing port): GigabitEthernet 0/2 Holdtime : 178 sec Version : Cisco Internetwork Operating System Software IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(13)EA1, RELEASE SOFTWARE (fc1) Copyright (c) 1986-2003 by cisco Systems, Inc. Compiled Tue 04-Mar-03 02:14 by yenanh advertisement version: 2 Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF000000000000000DBD064100FF0000 VTP Management Domain: “CISCO” Duplex: full
~~~
# Task 5:
NOTE: The show cdp neighbors detail command provides detailed information about devices. This is a very useful troubleshooting command as you can find out the IP addresses (and more) of connected devices and access them remotely. Try this command on Sw1 and see the information you find out about on R1. Familiarize yourself with the contents of this command for both routers and switches.
~~~
R1# configure terminal
Enter configuration commands, one per line. End with CTRL/Z.
R1(config)# interface GigabitEthernet 0/0
R1(config-if)#no cdp enable
Sw1(config)# no cdp run
~~~
# Task 6:
NOTE: The CDP entries will still remain until they time out. You can clear the entries with the clear cdp table command, and then issue show commands to check that there are no entries. Knowing how to disable CDP is an important security task for the CCNA exam.
# LLDP Configuration and Verification
## Lab Objective:
The objective of this lab exercise is for you to learn and understand how to enable the LLDP protocol on a Cisco Network.
## Lab Purpose:
Configuring and applying the Link Layer Discovery Protocol (LLDP) allows network devices to discover other network devices directly connected to them. This is a fundamental skill that provides the same benefits that CDP does, but it’s also compatible with non-Cisco equipment. As a Cisco engineer, as well as in the Cisco CCNA exam, you will be expected to know how to enable LLDP in your network.
## Lab Topology:
Please use the following topology to complete this lab exercise:
# Task 1:
Configure the hostnames on R1 and R3 as illustrated in the topology.
# Task 2:
Configure the IP addresses on the Ethernet interfaces of R1 and R3 as illustrated in the topology. There is no need to configure the Loopback interfaces for this lab.
# Task 3:
Disable CDP globally on both routers and enable LLDP (it’s disabled by default).
# Task 4:
Make sure that both R1 and R3 have found each other via their Ethernet links using LLDP.
# Task5:
Now disable one of the interfaces to prevent it from sending LLDP traffic.
# Task 1:
For reference information on configuring IP addresses, please refer to earlier labs.
# Task 2:
For reference information on configuring IP addresses, please refer to earlier labs.
~~~
R1# configure terminal
Enter configuration commands, one per line. 
End with CTRL/Z.
R1(config)# no cdp run
R1(config)# lldp run
R1(config)# end
R3# configure terminal
Enter configuration commands, one per line. End with CTRL/Z. R3(config)#no cdp run R1(config)#lldp run R3(config)#end R3#
~~~
# Task 4:
~~~
R1#show lldp neighbors
Capability codes: (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other Device ID      Local Intf     Hold-time  Capability     Port ID R3  G0/0  120        R  G0/0 Total entries displayed: 1 
R3# show lldp neighbors
Capability codes: (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device   (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other Device ID  Local Intf Hold-time  Capability  Port ID R1 G0/0  120  R G0/0 Total entries displayed: 1
~~~
# Task 5:
~~~
Router(config-if)#no lldp transmit
~~~
# Congratulations! You have completed this lab

