Cisco EtherChannel allows us to bundle up to eight ports active between switches. The links must have the same speed, duplex setting, and VLAN configuration in other words, you can’t mix interface types and configurations into the same bundle.
![](https://github.com/A3lpha/CCNA_200-301_Workbook/blob/main/images/Picture2.png)
 
There are a few differences in configuring PAgP and LACP, but first, let’s go over some terms so you don’t get confused:
Port channeling – Refers to combining two to eight Fast Ethernet or two Gigabit Ethernet ports together between two switches into one aggregated logical link to achieve more bandwidth and resiliency.
EtherChannel – Cisco’s proprietary term for port channeling.
PAgP – This is a Cisco proprietary port channel negotiation protocol that aids in the automatic creation for EtherChannel links. All links in the bundle must match the same parameters (speed, duplex, VLAN info), and when PAgP identifies matched links, it groups the links into an EtherChannel. This is then added to STP as a single bridge port. At this point, PAgP’s job is to send packets every 30 seconds to manage the link for consistency, any link additions, and failures.
LACP (802.3ad) – This has the exact same purpose as PAgP, but it’s nonproprietary so it can work between multi-vendor networks.

# LAB 08: EtherChannel Configuration
## LAB OBJECTIVE AND ACTIVITIES:
This lab was written for Eve-ng Community, Pre-configured Lab can be downloaded from Course Page. The lab can also easily be completed using your own equipment or GNS3. Instructions. Open the accompanying Eve-ng Lab titled “EtherChannel Configuration Lab”.  
Follow the exercises below to complete this lab.

### Lab Objectives
You can enable your channel-group for each channel by setting the channel mode for each interface to either active or passive if using LACP.
When a port is configured in passive mode, it will respond to the LACP packets it receives, but it won’t initiate an LACP negotiation.
When a port is configured for active mode, the port initiates negotiations with other ports by sending LACP packets.
~~~
S1(config)#interface range gigabitEthernet 0/0 – 1
S1(config-if-range)#switchport trunk encapsulation dot1q
S1(config-if-range)#switchport mode trunk
~~~
All ports in your bundles must be configured the same, so I’ll configure both sides with the same trunking configuration. Now I can assign these ports to a bundle:
~~~
S1(config-if-range)#channel-group 1 mode ? active
Enable LACP unconditionally auto
Enable PAgP only if a PAgP device is detected desirable
Enable PAgP unconditionally on 
Enable Etherchannel only passive
Enable LACP only if a LACP device is detected 
S1(config-if-range)#channel-group 1 mode active
S1(config-if-range)#exit
S1(config)#int port-channel 1
S1(config-if)#switchport trunk encapsulation dot1q
S1(config-if)#switchport mode trunk
S1(config-if)#switchport trunk allowed vlan 1,2,3
S2(config)#interface range gigabitEthernet 0/0 – 1
S2(config-if-range)#switchport trunk encapsulation dot1q
S2(config-if-range)#switchport mode trunk
S2(config-if-range)#channel-group 1 mode active
S2(config-if-range)#exit
S2(config)#int port-channel 1
S2(config-if)#switchport trunk encapsulation dot1q
S2(config-if)#switchport mode trunk
S2(config-if)#switchport trunk allowed vlan 1,2,3
~~~
Time to configure the interfaces, channel groups, and port channel interface on the S2 switch:
Let’s verify our EtherChannel with a few commands.
~~~
show etherchannel port-channel
~~~
## Layer 3 EtherChannel
You can use layer 3 EtherChannel when connecting a switch to multiple ports on a router, for example. It’s important to understand that you wouldn’t put IP addresses under the physical interfaces of the router, instead you’d actually add the IP address of the bundle under the logical port-channel interface.
~~~
Router# configure terminal 
Router(config)# interface port-channel 1 
Router(config-if)# ip address 10.1.1.1 255.255.255.0
Now we need to add the physical ports into port channel 1:
Router(config-if)#interface range G0/0-1
Router(config-if-range)# channel-group 1 gigabitEthernet 0/0
added as member-1 to port-channel1 gigabitEthernet 0/1 added as member-2 to port-channel1
~~~
Congratulations! You have completed this lab.

