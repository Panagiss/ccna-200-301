# Router
- A router provides connectivity between different IP subnets
- An IP address must be configured on the interfaces in each subnet

*interface FastEthernet0/0*

*ip address 192.168.0.1 255.255.255.0*

*no shutdown*

*interface FastEthernet0/1*

*ip address 192.168.1.1 255.255.255.0*

*no shutdown*

*show ip route -* in order to see the routing table of a Router


# Switch

- A Layer 2 Switch is not IP routing aware.
- It does however support a single IP address for management.
- The IP address and subnet mask is configured on the Switched Virtual Interface (SVI) for the default VLAN 1
- A default gateway also needs to be configured to allow connectivity to other subnets

*Switch(config)# interface vlan 1*

*Switch(config-if)# ip address 192.168.0.10 255.255.255.0*

*Switch(config-if)# no shutdown*

*Switch(config-if)# exit*

*Switch(config)# ip default-gateway 192.168.0.1*


Hostname

A descriptive hostname makes it easier to identify the device.

Eg. NY-F1-SW1

*Switch(config)# hostname SW1*

*SW1(config)#*



Interface descriptions can aid troubleshooting

*SW1(config)# interface FastEthernet 0/1
SW1(config-if)# description Link to R1*



# Router & Switch


- Interface speed and duplex is set to ‘auto’ by default
- Both sides of a link should auto-negotiate to full duplex and the fastest available speed
- Best practice is to manually set the speed and duplex on ports which are connected to another network infrastructure device or server
- It is very important to set matching speed and duplex settings on both sides of the link

*SW1(config)# interface FastEthernet 0/1*

*SW1(config-if)# duplex full*

*SW1(config-if)# speed 100*


*SW1# show running-config*

*SW1# show ip interface brief*

*SW1# show run interface vlan 1*

*SW1# show interface vlan 1*

*SW1# show version*



# CDP Cisco Discovery Protocol
- Cisco Discovery Protocol (CDP) is a Cisco proprietary Layer 2 protocol.
- It is used to share information with other directly connected Cisco equipment, such as the operating system version and IP address.
- This aids in troubleshooting by allowing administrators to map out how Cisco devices are connected to each other.
- It is enabled by default on most Cisco equipment.
- It works at Layer 2 so it is not necessary for the device to have an IP address.

*Switch(config)# cdp run*

*Switch(config)# no cdp run*

*Switch(config-if)# no cdp enable*

*Switch# show cdp*

*Switch# show cdp neighbors*

*Switch# show cdp neighbors detail*



# LLDP Link Layer Discovery Protocol

LLDP (Link Layer Discovery Protocol) is an open standard protocol which provides similar information to CDP.
Differences with CDP:

- Depending on the switch and version it may be disabled by default
- It is only supported on physical interfaces
- It can only discover up to one device per port
- It can discover Linux servers

*Switch(config)# lldp run*

*Switch(config)# no lldp run*

*Switch(config-if)# no lldp transmit*

*Switch(config-if)# no lldp receive*

*Switch# show lldp*

*Switch# show lldp neighbors*

*Switch# show lldp neighbors detail*


# Cisco Device Memory

Cisco routers and switches have 4 built-in memory locations:

- ROM – Read Only Memory
- Flash – newer devices use removable CompactFlash
- NVRAM – Non-Volatile RAM
- RAM – Random Access Memory
- An external USB device can also be used


# Factory Reset
To factory reset a router or switch: *write erase*

This will erase the startup-config

Reload to boot up with a blank configuration

The Setup Wizard will run


# The Config Register
- The configuration register can be used to change the way the router
- boots
- Use the *config-register* command in global configuration mode or *confreg* at the rommon prompt
- Eg *config-register 0x2142*

- 0x2102: boot normally (default)
- 0x2120: boot into rommon
- 0x2142: ignore contents of NVRAM (startup-config)


# Router Password Recovery Procedure

- Press the break sequence (Ctrl-Break) at power on to break into rommon prompt
- *confreg 0x2142* to ignore the startup-config on boot
- The startup-config is still there with the full configuration including the unknown enable secret, but the router does not use it when it boots
- *reset* to reload
- The router will bootup with no configuration. Type no to bypass the setup wizard
- Enter enable mode. You will not be prompted for the enable secret as it is not in the running configuration
- Copy the startup config to the running config
- This will copy the entire previous configuration into the running config including the unknown enable secret. You are already in enable mode so you do not need to know what it is.
- Enter a new *enable secret* in global configuration mode to overwrite the old one. This will go into the running config
- *config-register 0x2102* so the router will boot normally on the next restart
- *copy run start* to save the configuration. This will merge the new enable password into the existing startup-config


# Backing up the System Image and Config

- Copies of the device’s IOS system image and configuration can be saved to Flash, FTP, TFTP or USB
- If you copy a config file into the running-config, it will be merged with the current configuration
- To replace a configuration, factory reset and then copy the new configuration into the startup-config

*copy flash tftp*

*copy running-config tftp*

*copy startup-config usb*


# Upgrading the IOS System Image
- IOS software images can be downloaded from: https://software.cisco.com/
- After downloading the software, copy to the device’s Flash using TFTP: *copy tftp flash*
- Delete the old system image or use the *boot system* command


# Static Routers - Routers
*ip route 10.0.1.0 255.255.255.0 10.0.0.1*

Default gateway - *ip route 0.0.0.0 0.0.0.0 ADDRESS*



# Dynamic Routing Protocols Types
![](images/Configure_Routers-Switches/Aspose.Words.aefc82de-89dd-4d92-b629-9ac282c9f800.001.png)

**Routing protocols can be split into two main types**:

1. Interior gateway protocols (IGPs)
1. Exterior gateway protocols (EGPs)

Interior gateway protocols are used for routing within an organisation

Exterior gateway protocols are used for routing between organisations

over the Internet

The only EGP in use today is BGP (Border Gateway Protocol)

**Interior gateway protocols can be split into two main types**:

1. Distance Vector routing protocols
1. Link State routing protocols

## Distance Vector Routing Protocol
- In Distance Vector protocols, each router sends its directly connected neighbours a list of all its known networks along with its own distance to each of those networks
- Distance vector routing protocols do not advertise the entire network topology
- A router only knows its directly connected neighbours and the lists of networks those neighbours have advertised. It doesn’t have detailed topology information beyond its directly connected neighbours
- Distance Vector routing protocols are often called ‘Routing by rumour’
## Link State Routing Protocol
- In Link State routing protocols, each router describes itself and its interfaces to its directly connected neighbours
- This information is passed unchanged from one router to another
- Every router learns the full picture of the network including every router, its interfaces and what they connect to


Command to check Ip protocol in use for a router: *show ip protocols*

## Rip
- The Routing Information Protocol (RIP) is a Distance Vector routing protocol
- It uses hop count as its metric
- The maximum hop count is 15
- It will perform Equal Cost Multi Path, for up to 4 paths by default


*router rip* 

*version 2*

*no auto-summary*

*network 10.0.0.0*

The ‘network’ command should reference a classful network. No subnet

mask is specified


To watch live and debug use: *debug ip rip*

To find rip config: 

*show run  | section rip*

*show run  | begin rip*

To show the info Rip has found: 

*sh ip rip database*



RIP will automatically summarise routes to the classful boundary by default


For example, 192.168.10.1/30 will be advertised as 192.168.10.0/24

172.16.10.1/30 will be advertised as 172.16.0.0/16

This is almost never desirable

So:
*R1(config)#router rip*

*R1(config-router)#no auto-summary*

Manual summarisation gives you control of exactly how you summarise

The individual summarised routes are not advertised - only their summary

route
*R2(config-router)# interface f1/0*

*R2(config-if)# ip summary-address rip 10.0.0.0 255.255.0.0*


Default Route Injection (no need to manually set default route on each of the routers)

In our example R4 is connected to the Internet

*R4(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.2*

*R4(config)#router rip*

*R4(config-router)#default-information originate*


## EIGRP
- EIGRP (Enhanced Interior Gateway Routing Protocol) is an Advanced Distance Vector routing protocol
- It supports large networks
- It has very fast convergence time
- It supports bounded updates where network topology change updates are only sent to routers affected by the change
- Messages are sent using multicast
- EIGRP will automatically perform equal cost load balancing on up to 4 paths by default
- This can be increased up to 16 paths
- EIGRP can also be configured to perform unequal cost load balancing


*R1(config)#router eigrp 100*

‘100’ in this example is the Autonomous System (AS), meaning

an independent administrative domain. EIGRP routers need to

have the same Autonomous System number to peer with each

other.

*R1(config)#router eigrp 100*

*R1(config-router)#network 10.0.0.0 0.0.255.255*

- EIGRP routers identify themselves using an EIGRP Router ID which is in the form of an IP address.
- This will default to being the highest IP address of any loopback interfaces configured on the router, or the highest other IP address if a loopback does not exist.
- Loopback interfaces never go down so the Router ID will not change.
- You can also manually specify the Router ID.
- Best practice is to use a Loopback or manually set the Router ID

*R1(config-router)#eigrp router-id 2.2.2.2*


EIGRP Verification:

*R1#show run | section eigrp*

*R1#show ip eigrp interfaces*

*R2#show ip eigrp neighbors*


![](images/Configure_Routers-Switches/Aspose.Words.aefc82de-89dd-4d92-b629-9ac282c9f800.002.png)



## OSPF
*R1(config)#router ospf 1*

*R1(config-router)# network 10.0.0.0 0.0.255.255 area 0*
The network command means:

- Look for interfaces with an IP address which falls within this range.
- Enable OSPF on those interfaces – send out and listen for OSPF hello messages, and peer with adjacent OSPF routers.
- Advertise the network and mask which is configured on those interfaces.


OSPF Verification – show run | section ospf

*R1#sh run | section ospf*

*R1#show ip protocols*

OSPF Verification – show ip ospf interface brief

*R2#show ip ospf interface brief*

OSPF Verification - show ip ospf neighbor

*R2#show ip ospf neighbor*

OSPF Verification - show ip ospf database

*R2#show ip ospf database*

OSPF Verification - show ip route

*R2#show ip route*


OSPF Router ID

- OSPF routers identify themselves using an OSPF Router ID which is in the form of an IP address.
- This will default to being the highest IP address of any loopback interfaces configured on the router, or the highest other IP address if a loopback does not exist.
- Loopback interfaces never go down so the Router ID will not change.
- You can also manually specify the Router ID.
- Best practice is to use a Loopback or manually set the Router ID.

Router ID manual config

*R1(config-router)#router ospf 1*

*R1(config-router)#router-id 2.2.2.2*

% OSPF: Reload or use "clear ip ospf process" command, for this to take effect

*R1#clear ip ospf process*

*R1#show ip protocols*


Passive interface config

*R1(config)#router ospf 1*

*R1(config-router)#passive-interface loopback 0*

*R1(config-router)#passive-interface f2/0*

OR

*R1(config)#router ospf 1*

*R1(config-router)#passive-interface default*

*R1(config-router)#no passive-interface f0/0*

*R1(config-router)#no passive-interface f1/0*

*R1(config-router)#no passive-interface f3/0*

Default Route Injection

*R4(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.2*

*R4(config)#router ospf 1*

*R4(config-router)#default-information originate*






Bandwidth vs Speed/Clock

- The ‘bandwidth’ setting on an interface does not affect the physical transmission rate – that is set by the ‘speed’ or ‘clock rate’
- If you set a bandwidth of 50 Mbps on a FastEthernet interface, it will still transmit at 100 Mbps

OSPF Cost

- The cost is automatically derived from the interface bandwidth 
- Cost = Reference Bandwidth / Interface Bandwidth
- The default reference bandwidth is 100 Mbps
- FastEthernet link cost defaults to 1 (100 / 100)
- T1 link cost defaults to 64 (100 / 1.544)



OSPF treats all interfaces of 100 Mbps or faster as equal

FastEthernet, Gigabit Ethernet, 10 Gigabit Ethernet etc. all default to a cost of 1

This can cause undesirable routing in modern networks

*R1(config)#router ospf 1*

*R1(config-router)#auto-cost reference-bandwidth 100000* (100Gbps)


Manipulating the OSPF Metric (Cont.)

- If you want to use a different path, you can manipulate this by manually changing the bandwidth or OSPF cost on interfaces
- It is recommended to use cost because the bandwidth setting can affect many features other than OSPF (such as QoS)


OSPF Metric - Bandwidth

*R1#show interface serial1/0*

*Serial1/0 is administratively down, line protocol is down*

*Hardware is M4T*

*MTU 1500 bytes, BW 1544 Kbit/sec, DLY 20000 usec,*

*reliability 255/255, txload 1/255, rxload 1/255*

*!*

*R1(config)#interface serial1/0*

*R1(config-if)#bandwidth 768*

*!*

*R1#show interface serial1/0*

*Serial1/0 is administratively down, line protocol is down*

*Hardware is M4T*

*MTU 1500 bytes, BW 768 Kbit/sec, DLY 20000 usec,*

*reliability 255/255, txload 1/255, rxload 1/255*

OSPF Metric - Cost

A manually configured OSPF cost overrides the value

automatically derived from the bandwidth

*R1(config)#interface FastEthernet 0/0*

*R1(config-if)#ip ospf cost 50*

*R1#show ip ospf interface FastEthernet 0/0*




DR and BDR

- A DR Designated Router and BDR Backup Designated Router are elected
- The router with the highest priority becomes DR, and the router with the 2nd highest priority becomes BDR
- Default priority is 1, the higher the better (0 - 255)
- Highest Router ID is used in case of a tie
- On multiaccess segments such as Ethernet, the routers elect the DR and BDR at the 2-Way stage
- There is no election on point to point links

*R1(config)#interface FastEthernet 0/0*

*R1(config-if)#ip ospf priority 100*

*R4(config)#interface FastEthernet 0/0*

*R4(config-if)#ip ospf priority 0*


*R4#clear ip ospf process*



OSPF Router Types - ABRs

An ABR has the following characteristics:

- It separates LSA flooding zones.
- It becomes the primary point for area address summarization.
- It functions regularly as the source for default routes.
- It maintains the LSDB for each area with which it is connected.
- The ideal design is to have each ABR connected to two areas only, the backbone and another area, with three areas being the upper limit

*R2(config)#router ospf 1*

*R2(config-router)#network 10.1.0.0 0.0.255.255 area 0*

*R2(config-router)#network 10.0.0.0 0.0.255.255 area 1*

*R2(config-router)#area 0 range 10.1.0.0 255.255.0.0*

*R2(config-router)#area 1 range 10.0.0.0 255.255.0.0*
# Loopbacks
*config t*

*interface loopback 0*

# Passive Interface

The passive-interface command has the same effect on our routing protocols which is to prevent routing updates.

For OSPF and EIGRP, the command stops hello packets from being sent. Therefore, it will not discover any neighbors which results in prevention of routing updates, both outgoing and incoming.

For RIP, the command will disable the interface from sending multicast updates. However, it is still able to receive incoming updates.

*router rip
passive-interface f0/0*

*network 203.0.113.0* 


# Troubleshoot
1. **Layer 1**
   1. *Show ip interface brief*
   1. *Show interface*
1. **Layer 2**
   1. *Show arp*
   1. *Show mac address-table*
1. **Layer 4**
   1. *Telnet*
1. **Dns**
   1. *nslookup*
   1. *Ping by FQDN*
