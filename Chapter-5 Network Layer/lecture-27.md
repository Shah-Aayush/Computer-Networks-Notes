# Lecture 27

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/d9252BrQZus)|

---

- to manage backbone of subnets
- connection-less subnet : packet will be transmitted independently; packet transmits independent of the previous packets.
- connection-oriented subnet : connection should be established; same path should be followed by packets
- tasks of network : 
	- routing, congesion control, connection establishment
	- contention (not for network layer) : fighting for a single resource
	- congesion (for network layer): traffic jam, over crowded network
	- providing quality of service
		- reliability
		- timely delivery; no delay
	
- Network Layer Design Issues
	```
	• Store-and-forward packet switching
	• Services provided to transport layer
	• Implementation of connectionless service | datagram subnet
	• Implementation of connection-oriented service | virtual circuit
	• Comparison of virtual-circuit and datagram networks	
	```

- ## Store-and-Forward Packet Switching

	- network doesn't deal with process to process computer. its the work of transport layer. network layer works with computer to computer communication.
	- job of network layer is to manage subnet

- ## Services Provided to the Transport Layer
	```
	• Services independent of router technology.
		> compony/specs should not be barrier.
	• Transport layer shielded from number, type,
	topology of routers.
	• Network addresses available to transport layer use uniform numbering plan 
		> even across LANs and WANs
	```
	- transport layer should not be involved in the management of routers. it should be done by network layer.

- Implementation of Connectionless Service **[Applicable to IP]**

	- no connection establishment. every computer will decide itself that to which computer it should transfer the packet now?.
	- every router is supposed to maintain routing table.
	- routing algo : 
		- static routing : manually feed
		- dynamic routing : gradually learns table itself.
	
- Implementation of Connection-Oriented Service
	- no ip
	- reliable connection
	- before transmission, first we should establish connection
	- first transmission is of **CONTROL** packet.
		- routed packet
	- every packet will have just a connection number and every packet will follow that.
	- same path followed by all the same numbered connection.
	- this is logical path
	- if any fault occurs, then the new connection will be formed by  the host. all the previous connection, packets will be dropped and remaining packets will be routed to all new connection.

	- sequence  number will be uniquely identified. and  will be valid only for one transmission. 
		- no sequence number should be repeated.
		- it will be valid only for one  transmission.
		- no simultanous tranmission.
		
- Routing Algorithms (1)
	```
	• Optimality principle
	• Shortest path algorithm
	• Flooding | very famous
	• Distance vector routing | widely used
	• Link state routing
	• Routing in ad hoc networks
	• Broadcast routing
	• Multicast routing
	• Anycast routing
	• Routing for mobile hosts
	```

- Routing vs Forwarding
	- routing : making a decision which route to use
		- also maintaining table
	- forwarding : actually forwarding packet to the path

	```
	• Routing is making the decision which routes to use, and forwarding, is what happens when a packet arrives
	• Router has two processes inside it. One of them handles each packet as it arrives, looking up the outgoing line to use for it
	in the routing tables. This process is forwarding. The other process is responsible for filling in and updating the routing tables.
	```