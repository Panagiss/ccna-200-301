# **DHCP – Dynamic Host Configuration Protocol**
- DHCP is a client/server protocol that automatically provides a host with its IP address and other related configuration information such as the subnet mask and default gateway.
- DHCP clients obtain their IP configuration information from a DHCP server, rather than being manually configured.


- Centralized and automated IP configuration, rather than manually assigning an IP address to every host.
- Can assign additional IP configuration values by means of DHCP options.
- Efficient handling of clients that must be updated frequently, such as laptops that move to different locations on a wireless network.
- The forwarding of initial DHCP messages by using a DHCP relay agent, which eliminates the need for a DHCP server on every subnet.
- DHCP minimizes configuration errors caused by manual IP address configuration, such as typos, or address conflicts caused by the assignment of an IP address to more than one computer at the same time.

# **DHCP Clients**
- Desktop PCs are good candidates to be DHCP clients because there will typically be many of them in an office. Using DHCP saves a lot of admin work that would be necessary if manually configuring IP addresses.
- They do not accept incoming connections so it does not matter if their IP address changes.
- Servers and network infrastructure devices such as routers and switches will **not** typically be DHCP clients.
- They are mission critical devices which do not move and are required for the network and its services to function.
- Their IP addresses are manually configured to ensure they will not change and are not dependent on DHCP.


# **Cisco DHCP Server Configuration**
*R1(config)#ip dhcp excluded-address 10.10.10.1 10.10.10.10*

*R1(config)#ip dhcp pool 10.10.10.0\_Clients*

*R1(dhcp-config)#network 10.10.10.0 255.255.255.0*

*R1(dhcp-config)#default-router 10.10.10.1*

*R1(dhcp-config)#dns-server 10.10.20.10*

*R1#show ip dhcp pool*

*R1#show ip dhcp binding*



External DHCP Server Configuration

*R1(config)#interface f0/1* (The incoming interface)

*R1(config-if)#ip helper-address 10.10.20.10*



# **Cisco Router as a DHCP Client**
- Cisco routers are typically manually configured with static IP addresses
- An exception to this is where an office is connected to the Internet but has not bought static public IP addresses (because it does not contain any publicly available servers which would need a fixed IP address for incoming connections)
- The office still requires a public IP address to allow internal hosts outbound connectivity to the Internet through NAT
- In this case the router will receive the public IP address on its outside interface from the Internet service provider via DHCP

*R1(config)#interface f0/0*

*R1(config-if)#ip address dhcp*

*R1(config-if)#no shutdown*

*R1#show dhcp lease*
