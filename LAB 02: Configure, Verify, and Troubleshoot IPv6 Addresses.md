# LAB OBJECTIVE AND ACTIVITIES:
The objective of this lab exercise is for you to learn and understand how to create and troubleshoot Ipv6 addresses on Cisco routers.

# Lab Purpose:
Configuring IPv6 addressing is one of your most fundamental tasks as a Cisco engineer. In the exam, you may also be asked to troubleshoot IPv6 addressing that has been incorrectly configured, so you need to know which show commands to use.

# Lab Topology:
Please use the following topology to complete this lab exercise:

# Task 1:
Configure the hostnames on routers R1 and R2 as illustrated in the topology.

# Task 2:
Configure the IP addresses on the interfaces of R1 and R2 as illustrated in the topology. Configure the Loopback interfaces specified in the diagram on R1 and R2.

# Task 3:
Use the correct show commands to check:

The summary of all configured IPv6 addresses (note the need to specify IPv6 in the show commands);
The status of the interface (up/down or administratively down); and
The subnet mask applied to the interface.
Configuration and Verification
Task 1:  
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
# Task 3:
~~~
~~~
R2(config)# ipv6 unicast-routing
R2(config)# interface GigabitEthernet 0/0
R2(config-if)# ipv6 add 2001:abcd:abcd::2/64
R2(config-if)# no shutdown
R2(config)# interface loopback 0
R2(config-if)# ipv6 add 2001::5/64
~~~
~~~
R2# show ipv6 interface brief 
~~~
Congratulations! You have completed this lab.
