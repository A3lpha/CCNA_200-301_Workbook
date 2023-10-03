# LAB 04: Cisco Switch Configuration
LAB OBJECTIVE AND ACTIVITIES:
Switches are one of the most numerous devices installed onto the corporate network infrastructure. Configuring them can be fun and challenging.
Knowing how switches normally boot and load an operating system is also important.
~~~
Help Commands
switch> enable
~~~
Enters privileged EXEC mode
~~~
switch> configure terminal
Enters global configuration mode
switch(config)# no ip domain-lookup
~~~
Turns off DNS queries so that spelling mistakes do not slow you down
~~~
switch(config)# hostname SW1
~~~
Sets the host name
~~~
SW1(config)# enable secret hurbad
~~~
Sets the encrypted secret password to hurbad
~~~
SW1(config)# line console 0
Enters line console mode
SW1(config-if)# logging synchronous
~~~
Appends commands to a new line; switch information will not interrupt
~~~
SW1(config-if)# password switch
Sets the console password to switch
SW1(config-if)# login
User must log in to console before use
SW1(config-if)# exec-timeout 0 0
~~~
The console line will not log out because of the connection to the console being idle
~~~
SW1(config-if)# exit
~~~
Moves back to global configuration mode
~~~
SW1(config)# line vty 0 15
~~~
Moves to configure all 16 vty ports at the same time
~~~
SW1(config-if)# password class
~~~
Sets the vty password to class
~~~
SW1(config-if)# login
~~~
User must log in to vty port before use
~~~
SW1(config-if)# exit
~~~
Sets default gateway address
~~~
SW1(config)# ip default-gateway 192.168.1.1
SW1(config)# interface vlan 1
~~~
Moves to virtual interface VLAN 1 configuration mode
~~~
SW1(config-if)# ip address 192.168.1.2 255.255.255.0
Sets the IP address and netmask for switch
SW1(config-if)# no shutdown
Turns the virtual interface on
SW1(config-if)# interface GigabitEthernet 0/0
~~~
Moves to interface configuration mode for GigabitEthernet 0/0
~~~
SW1(config-if)# description Link to Hurbad-HQ Router
~~~
Sets a local description
~~~
SW1(config-if)# description Link to to Workstation A
~~~
Sets a local description
~~~
SW1(config)# interface GigabitEthernet 0/2
~~~
Moves to interface configuration mode for Gigabitethernet 0/2
~~~
SW1(config-if)# interface GigabitEthernet 0/1
~~~
Moves to interface configuration mode for Gigabitethernet 0/1
~~~
SW1(config-if)# description Link to to Workstation B
~~~
Sets a local description
~~~
SW1(config-if)# exit
~~~
Returns to global configuration mode
~~~
SW1(config)# exit
~~~
Returns to privileged EXEC mode
~~~
SW1# copy running-config startup-config
~~~
## Congratulations! You have completed this lab.
Saves the configuration to NVRAM
Congratulations! You have completed this lab.

