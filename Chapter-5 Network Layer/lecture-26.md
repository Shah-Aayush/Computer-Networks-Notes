# Lecture 26

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/hmrJPIf_FWM)|

---

## IP Version 4 Protocol (1)

each line 32 bit | 4 byte

- version : v4 or v6
- IHL : Ip Header Link : 20 bytes : 5 lines : 4*5 bytes
- base header 20 bytes fixed
- options are optional : 0 to 40 words
- min : 20, max : 60 (20 fixed + 40 words) bytes.
- min length of IHL : is `0101` and max is `1111` as  `5*4 = 20` bbytes which is minimum, and `15*4 = 60` which is maximum.
- differentiated services : priority, qos handling
	> qos : quality of service
- total length : header + payload (tcp/udp packet)
- identification : sequence number
	> IP doesn't have ACK.
	> highly unreliable service | Datagram service : connection less
	
DF : don't fragment
fragment : breaking the packet in smaller pieces
DF: 0 : if required router can fragment.
DF:1 : router cannot fragment the packet.

MF : more fragment
mf:0 : last fragment
mf:1 : more fragment coming...

fragment offset : relative fragment position
seq. no will be same of all fragment.
second line is totally for fragmentation

ttl : time to live : age of the packet : hop count 
ttl:10 : packet can travel through 10 routers.
whenever ttl becomes 0 that packet will be discarded by the router.

- protocols : what follows the base header
	tcp  : protocols=6
	udp : protocols=23

- header checksum : to protect the header
- source and destination address : 32 bit ip address

- Options in IP
	> this will have another field header; placed after the base header
	- Security : to protect the IP packet
	- Strict source routing : 
	- Loose source routing : 
	> to override power given to the router; decide the path to be followed by that router
	-  record route : record the path followed by router
	- timestamp : along with ip address, it also records time
	
- Initial prefix : Network address
	> this will be same of all device of specific organization network
- Later part : Host address
- proportion of these two can be different.

- to know length of network, `subnet mask` is used.
	- 255.0.0.0 : 
		- 2^(8)-1
		- 11111111.00000000.00000000.00000000
		- 8 bits network; 24 bits host
		- /8
			> first 8 bits are `1`, later are `0`s
		
	- nirma subnet mask : 255.255.0.0
		- ip : 10.1.32.10
		- *extracted* Network address : 10.1.0.0
		- subnet mask bits will be included in network bits.
		
- Class A
	- /8
	- first bits : 0
	- ALL ZEROS CANNOT USED IN NETWORK
	- 1.0.0.0 to 127.255.255.255
	
- Class B
	- /16
	- first bits : 10
	- 128.0.0.0 to 191.255.255.255
	
- Class C
	- /24
	- first bits : 110
	- 192.0.0.0 to 223.255.255.255

- Class D
	- /24
	- first bits : 1110
	- 224.0.0.0 to 239.255.255.255
	- This ip cannot be assigned to a PC. not ip add. for computer
	- No breakup for network/host
	- pc group
	- multiclass address
	
- Class E
	- /32
	- first bits : 1111
	- not being used anywhere
	- reserved for future use
	
- special address
	- quad zeros : unspecified address : 0.0.0.0
		> current computer
	- network address part : 0
		> current network
	
		> a host on this network
	- 255.255.255.255 : broadcast address
		> this is local broadcasting
	- network (any) + host = 111111...
		> broadcast on a distant network ; remote broadcast
	
		> get in some specified network and then broadcast in that address
	- 127 + (anything) : Loopback
		> 127.0.0.1 : local host
		- self computer
		- application layer -> network layer -> transport layer : detects self computer ip -> reverse direction and go to application layer. not do to datalink layer
		- used to test your protocol stack
		
	
- ## COOL TRICK  
	- Local Disk C / windows/ system 32 /drivers/ etc/host
	- open this file
	- we can change ip and and redirecting website through this.
	- like :
		`216.239.32.20 : www.google.ac`
		convert it to
		`216.239.32.20 : www.youtube.com`
		then we can never `visit youtube.com`. it will always redirect us to google.com
	- this is a local host DNS server file