# Lecture 3

- Ethernet is always **Broadcasting**.
- interconnected processors by scale : 
	1. Personal Area Network		*1-10m*
	2. Local Area Network			*10m-1km*
	3. Metropolitan Area Network	*10km*
	4. Wide Area Network			*100km-1000km*
	5. The Internet					*10000km*

- Transmission Technology : 
	1. Broadcast links
	2. Point-to-point links
- Broadcasting channel : 
	- Unicast [both]
		> one to one
	- Multicast [both]
		> one to group of many but sends to specific numbers only
	- Broadcast	[only supported by ipv4]
		> sends to all receivers
		> *can be supported by ipv6 as special case of Multicast*
	- Anycast [only supported by ipv6]
		> sends to group of some but received by only one of them.

	```
	Ethernet : 802.3
	MAN : 802.6
	WIFI : 802.11
	Bluetooth : 802.15
	```
	
	Junction box : used for splitting network
	
	