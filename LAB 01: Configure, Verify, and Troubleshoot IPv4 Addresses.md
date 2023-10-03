THIS LAB OBJECTIVE AND ACTIVITIE:
The objective of this lab exercise is for you to learn and understand how to create and troubleshoot IPv4 addresses on Cisco routers.

Lab Purpose:
Configuring IPv4 addressing is one of your most fundamental tasks as a Cisco engineer. In the exam, you may also be asked to troubleshoot IPv4 addressing that has already been configured but incorrectly, so you need to know which show commands to use.

Lab Topology:
Please use the following topology to complete this lab exercise:

# Task 1:
Configure the hostnames on routers R1 and R2 as illustrated in the topology.

# Task 2:
Configure the IP addresses on the interfaces of R1 and R2 as illustrated in the topology. Configure the Loopback interfaces specified in the diagram on R1 and R2.

# Task 3:
Use the correct show commands to check:

The summary of all configured IP addresses;
The status of the interface (up/down or administratively down); and
The subnet mask applied to the interface.
Configuration and Verification
# Task 1:   
~~~
Router# configure terminal
Router(config)# hostname R1
R1(config)# Router# configure terminal
Router(config)# hostname R2
R2(config)#
~~~
# Task 2:
~~~
R1(config)#interface GigabitEthernet 0/0
R1(config-if)#ip add 172.16.1.1 255.255.255.0
R1(config-if)#no shutdown
R2(config)#interface GigabitEthernet 0/0
R2(config-if)#ip add 172.16.1.2 255.255.255.0
R2(config-if)# no shutdown
R2(config)#interface loopback 10
R2(config-if)#ip add 10.10.10.3 255.255.255.0
R2(config)#interface loopback 20
R2(config-if)#ip add 10.20.20.3 255.255.255.0
R2(config)#interface loopback 30
R2(config-if)#ip add 10.30.30.3 255.255.255.248
~~~
# Task 3:
~~~
R2# show ip interface brief
~~~

Congratulations! You have completed this lab.
