# Lecture 4
### [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=a932c5941fd38e9463effac01b834633)
### Password : `HpJPPjm4`

- Default gateway is the ip address of the router
- ISP : Internet service provider *[blazenet, reliance, jio, gtpl]*
- **Backbone network** : A backbone or core network is a part of a computer network which interconnects networks, providing a path for the exchange of information between different LANs or subnetworks. A backbone can tie together diverse networks in the same building, in different buildings in a campus environment, or over wide areas. *Also called as Subnet.*
- All WAN are connected internally somehow...
- Main job of WA over is to routing *(forwarding)* the packets over correct route.
- Virtual Private Network *VPN* : Secured link, shared network.
	
- **Intranet** : An intranet is a computer network for sharing information, collaboration tools, operational systems, and other computing services within an organization, usually to the exclusion of access by outsiders. *Within network*
	- **Intranet** : withing network
	- **Internet** : between networks
- Key Terms related to WAN : 
	1. Packet - Logical group of information *[Bits + Source Address + Destination Address]*
	2. Packet switching - copying of packets from one node to another node in router is called when routing is being performed.
		- Packet switching is an approach used by some computer network protocols to deliver data across a local or long-distance connection.
		- method of grouping data that is transmitted over a digital network into packets. 
		- Copying the data by bits by bits
			- *CKT : Circuit switching* : Telephone network : Dedicated physical channel established. *No need to make packets and give address as there is only one channel!* Individual bits can travel.
			- *PKT : Packet switching* : 
			
			- Mobile phone call; Internet call
				1. In Packet switching, there can be dataloss.
				2. GSM (*Global System for Mobile communications*) call is **CIRCUIT SWITCH** 
				(_Time is an issue here as we are acquiring some dedicated resources here_)
					- High quality
					- can be Inefficient 
				3. Whatsapp/Internet call is **Packet SWITCH** (_Here time is not an issue as we are not acquiring any resources. but data is an issue as we are sending data here_)
					- Less quality
					- can be Efficient 
				> So which is best among these two? : <u>DEPENDS ON APPLICATION is the answer!</u>
				
				
				
	3. Routing - identifying the best route is routing
		- finds by routing algorithms; routing tables
		- finds the best neighbour

	
	4. Datagram - Kind of subnets/ WANs	{Packet switch}
		- Connection less subnet
		> Don't Need to establish connection before sending any packets/ transmission
		> Path not fixed
		> Asking to someone and going somewhere
		> Dynamic path changing
		> Link/router fail cannot affect the transmission
		D subnets  (Datagram)
		> Ip protocol is connection less.
		> Destination ip address should be carried by every packet.
		
	5. Virtual Circuit	{Packet switch}
		- Connection oriented subnet
		> Need to establish connection before sending any packets
		> Logical connection established
		> Path fixed
		> Google maps directing
		> Link/Router fails can drop/terminate the connection.
		VC  (Virtual Subnets)
		> can be work like water flowing through pipe.
		> Connection number will be carried instead of carrying ip address of next router.
		> Not need to routing for subsequent packets.
		> Similar to circuit switching *(Not exactly like that)*
