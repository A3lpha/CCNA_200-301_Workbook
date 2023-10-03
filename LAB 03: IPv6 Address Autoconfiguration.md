# LAB 03: IPv6 Address Autoconfiguration
LAB OBJECTIVE AND ACTIVITIES:
The objective of this lab exercise is for you to learn and understand how to configure IPv6 addresses on Cisco routers using address autoconfiguration and EUI-64 addressing.
Lab Purpose:
Configuring IPv6 addressing is one of your most fundamental tasks as a Cisco engineer. In the exam, you may also be asked to configure an IPv6 address using Stateless Address Autoconfiguration (SLACC) as well as EUI-64 addressing.
Lab Topology:
Please use the following topology to complete this lab exercise:
# Task 1:
Configure the hostnames on routers R1 and R2 as illustrated in the topology.
# Task 2:
Configure the IP addresses on the interfaces of R1 and R2 as illustrated in the topology. Configure the Loopback interfaces specified in the diagram on R1 and R2.
G0/0 on R2 will use SLACC to obtain the address prefix from R1. Loopback0 will use EUI-64 to complete the host portion of the address.
# Task 3:
Use the correct show commands to check:
1.	The summary of all configured IPv6 addresses (note the need to specify IPv6 in the show commands);
2.	The status of the interface (up/down or administratively down); and
3.	The subnet mask applied to the interface.
Configuration and Verification
# Task 1:
~~~
Router# configure terminal
Router(config)# hostname R1
R1(config)#
Router# configure terminal
Router(config)# hostname R2
R2(config)#
~~~
# Task 2:
~~~
R1(config)# ipv6 unicast-routing
R1(config)# interface GigabitEthernet 0/0
R1(config-if)# ipv6 add 2001:abcd:abcd::1/64
R1(config-if)# no shutdown
~~~
# Task 3:
~~~
R2(config)# ipv6 unicast-routing
R2(config)# interface GigabitEthernet 0/0
R2(config-if)# ipv6 add autoconfig
R2(config-if)# no shutdown
R2(config)# interface loopback 0
R2(config-if)# ipv6 address 2001:aaaa:aaaa:aaaa::/64 eui-64
R2# show ipv6 interface GigabitEthernet 0/0
~~~
Congratulations! You have completed this lab.

