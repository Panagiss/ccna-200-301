# Class A
- First bit ALWAYS 0
- Default subnet mask is /8
- Network address range: 1.0.0.0 - 126.0.0.0 /8
- So 126 networks and 16.777.214 hosts per network

Also

0.0.0.0/8 reserved and signifies "this network", so 0.0.0.1 - 0.255.255.255 are NOT valid host addresses

And

127.0.0.0/8 is reserved as loopback address, so 127.0.0.1 - 127.255.255.255 are NOT valid host addresses


# Class B
- First two bits are always set to 10
- Default subnet is /16
- Valid network addresses: 128.0.0.0 - 191.255.0.0 /16
- 16.384 networks and 65.534 hosts per network



# Class C
- The first three bits are always 110
- Default subnet mask is /24
- Valid network addresses: 192.0.0.0 - 223.255.255.0 /24
- 2.097.152 networks and 254 hosts per network

# Private Addresses Ranges
Class A: 10.0.0.0 - 10.255.255.255
Class B: 172.16.0.0 - 172.31.255.255
Class C: 192.168.0.0 - 192.168.255.255

#
# Class D
- Reserved for multicast addresses
- First four bits are always 1110
- These addresses are not allocated to hosts and there is no default subnet mask
- Range: 224.0.0.0 - 239.255.255.255

# Class E
- Experimental and reserved for future use
- First four bits are always 1111
- Not allocated to hosts so there is no default mask
- Range 240.0.0.0 - 255.255.255.255
- 255.255.255.255 is the broadcast address for "this network"

