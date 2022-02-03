# **Network Redundancy**
![](images/Network_Redundancy-HSRP/Aspose.Words.d288ce6b-2660-4bd6-ae2c-d01060fe47f4.001.png)

- The point of redundancy is to eliminate single points of failure
- Now we have added redundant switches, routers and Internet connections
- We can still reach the Internet if any core/distribution layer switch, router or link fails

- We do not typically implement redundancy at the **access layer** because end hosts have only one network card
- Servers with redundant NICs are an exception


- Redundancy and failover are relatively easy to implement for Layer 3 routing
- Routes on R1:

Static route to SP1:

*ip route 0.0.0.0 0.0.0.0 203.0.113.1*

Backup default static route via R2 if link to SP1 goes down(5 is AD):

*ip route 0.0.0.0 0.0.0.0 10.10.20.2 5*

Backup route to inside via R2 if link to CD1 goes down:

*ip route 10.10.10.0 255.255.255.0 10.10.20.2*


# **Host Gateways FHRP**

- We have redundant gateways for the PCs in the 10.10.10.0/24 network:
  - R1 with IP address 10.10.10.2
  - R2 with IP address 10.10.10.3
- We could configure half our PCs to use 10.10.10.2 as their default gateway, and half to use 10.10.10.3
- That would be inconvenient and would require manual reconfiguration on the PCs


![](images/Network_Redundancy-HSRP/Aspose.Words.d288ce6b-2660-4bd6-ae2c-d01060fe47f4.002.png)

**First Hop Redundancy Protocols (FHRP)**

- First Hop Redundancy Protocols (FHRP) use a Virtual IP (VIP) and MAC address to allow for automated gateway failover
- The hosts use the VIP as their default gateway address
- If a physical gateway fails, another gateway will take over

**Different FHRP protocols**

1. Hot Standby Router Protocol (**HSRP**): Cisco proprietary. Deployed in active/standby pair.
1. Virtual Router Redundancy Protocol (**VRRP**): Open standard. Deployed in active/standby pair. Very similar to HSRP.
1. Gateway Load Balancing Protocol (**GLBP**): Cisco proprietary. Supports active/active load balancing across multiple routers.

# **HSRP (Hot Standby Router Protocol)**

- Both routers have a normal physical IP address and MAC address on their HSRP interface. Unique addresses are used on both routers.
- They both also have the HSRP virtual IP and MAC address configured on the interface. The same addresses are used on both routers.
- When they come online, one is elected the HSRP active router, the other is the standby
- The active router owns the virtual IP and MAC address and responds to ARP requests
- All traffic for the VIP goes through the active router
- The routers send hello messages to each over their HSRP interface
- If the standby router stops receiving hellos from the active it will transition to be the active router
- It will take ownership of the virtual IP and MAC address and respond to ARP requests

HSRP Configuration

*R1(config)#interface g0/1*

*R1(config-if)#ip address 10.10.10.2 255.255.255.0*

*R1(config-if)#no shutdown*

*R1(config-if)#standby 1 ip 10.10.10.1*

*R1#show standby*


Priority and Pre-emption

- You can choose which router will be the active by setting priority on the routers
- The router with the higher priority will be preferred (default is 100)
- In the event of a tie the highest IP address wins
- If pre-emption is also enabled, when a higher priority router comes back online after a failure it will transition back to active
- If pre-emption is not enabled (default), the lower priority router will remain active when the failed router comes back online
- This can be more stable if a higher priority router is flapping

*R1(config)#interface g0/1*

*R1(config-if)#ip address 10.10.10.2 255.255.255.0*

*R1(config-if)#no shutdown*

*R1(config-if)#standby 1 ip 10.10.10.1*

*R1(config-if)#standby 1 priority 110*

*R1(config-if)#standby 1 preempt*

*R2(config)#interface g0/1*

*R2(config-if)#ip address 10.10.10.3 255.255.255.0*

*R2(config-if)#no shutdown*

*R2(config-if)#standby 1 ip 10.10.10.1*

*R2(config-if)#standby 1 priority 90*


HSRP Version

- HSRP version 2 introduced a few minor improvements
- The default is version 1
- Both routers must be running the same version

*R1(config)#interface g0/1*

*R1(config-if)#ip address 10.10.10.2 255.255.255.0*

*R1(config-if)#no shutdown*

*R1(config-if)#standby 1 ip 10.10.10.1*

*R1(config-if)#standby version 2*

*R1#show standby*


**Active/Active’ HSRP**


10.10.10.0 Subnet

*R1(config)#interface g0/1*

*R1(config-if)#ip address 10.10.10.2 255.255.255.0*

*R1(config-if)#no shutdown*

*R1(config-if)#standby 1 ip 10.10.10.1*

*R1(config-if)#standby 1 priority 110*

*R1(config-if)#standby 1 preempt*

*R2(config)#interface g0/1*

*R2(config-if)#ip address 10.10.10.3 255.255.255.0*

*R2(config-if)#no shutdown*

*R2(config-if)#standby 1 ip 10.10.10.1*

*R2(config-if)#standby 1 priority 90*





10.10.20.0 Subnet

*R1(config)#interface g0/2*

*R1(config-if)#ip address 10.10.20.2 255.255.255.0*

*R1(config-if)#no shutdown*

*R1(config-if)#standby 1 ip 10.10.20.1*

*R1(config-if)#standby 1 priority 90*

*R2(config)#interface g0/2*

*R2(config-if)#ip address 10.10.20.3 255.255.255.0*

*R2(config-if)#no shutdown*

*R2(config-if)#standby 1 ip 10.10.20.1*

*R2(config-if)#standby 1 priority 110*

*R2(config-if)#standby 1 preempt*
