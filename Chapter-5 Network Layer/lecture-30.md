# Lecture 30

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/w7jNnLAsDpk)|

---

- ## Learning about the neighbours

	- Assume that : A, C, F are connected to a switch 
	- LAN can be replaced by a node *(Virtual node)*
	- At the time of making link state packets, we are suppose to know about everything by sending hello packet. *(this is reference topology)*
	- **ACK flags are opposite of Send flags**
	- Send flags are the nodes through which packets can come to given node, then given it a `0` number so that it represents that we don't have to flood that node. the fields in which send flags are set to 1, we have to flood packets in that node.
	- as `A`,`F` are direct neighbours of `B`, the TTL  (time to leave) value/ age of the packet will be 60 only.
	- but as `E` is not a direct neighbour of `B` and it has to come through different node (1 node between E and B), its TTL value/age will be decreased by 1. so it's `59`.

- ## Hierarchical routing
	- drawbacks of huge routing table
		- memory required
		- destination address of some arrived packet should be match with all thousands of router's entries in table.
			- every packet will take lot of time
			- more **processing power** will required and more **bandwidth** required
		- time Delay 
		
	- slides points : 
		```
		• As networks grow in size, the routing tables grow proportionally
		• Not only is router memory consumed by ever-increasing tables, but
		more CPU time is needed to scan them and more bandwidth is needed
		to send status reports about them.
		• The routers are divided into what we will call regions.
		• Two levels may not be sufficient for huge networks
		• It may be necessary to group the regions into clusters, the clusters into
		zones, the zones into groups
		• How many levels should the hierarchy have?
		• For example, consider a network with 720 routers. If there is no hierarchy, each
		router needs 720 routing table entries. If the network is partitioned into 24 regions of 30 routers each, each router needs 30 local entries plus 23 remote entries for a total of 53 entries. If a three-level hierarchy is chosen, with 8 clusters each containing 9 regions of 10 routers, each router needs 10 entries for local routers, 8 entries for routing to other regions within its own cluster, and
		7 entries for distant clusters, for a total of 25 entries.
		```
	
	- LEVELS : 
		1. Local
		2. Regions
		3. Clusters
		4. Zones
		5. Groups
	
	- number of entries in every levels can be different.
	- **IP uses : Route Agreegation **
		- Hierarchical Routing
	
- ## Broadcast Routing
	- slide points
	```
		• Sending a packet to all destinations simultaneously is called broadcasting
		• One broadcasting method that requires no special features from the network is for the source to simply send a distinct packet to each destination. > Multiple unicasting
		• An improvement is multidestination routing, in which each packet contains either a list of destinations or a bit map indicating the desired destinations.
		• When a packet arrives at a router, the router checks all the destinations to determine the set of output lines that will be needed. The router generates a new copy of the packet for each output line to be used and includes in each packet only those destinations that are to use the line
		• A better broadcast routing technique is flooding
	```
	
	- creating 100s of packets and assigning a single destination ip address to it to broadcast is called **Multiple unicasting**.
		- costly alternative
	- **Multidestination routing**
		- 100s of network addresses in single packet.
		
- ## Broadcast routing - reverse path forwarding
	- optimised version of broadcasting
	- **flooding is the most optimised algorithm for finding shortest path**
	- the nodes which are not circled are not joining it's above node *(shortest path not considered although it has a path)*
		- here `L` doesn't join `B` but it joins `K`. which is shortest path for it.
	- slide points
		```
		• When a broadcast packet arrives at a router, the router checks to see if the packet arrived on the link that is normally used for sending packets toward the source of the broadcast.
		• If so, there is an excellent chance that the broadcast packet itself followed the best route from the router and is therefore the first copy to arrive at the router.
		• This being the case, the router forwards copies of it onto all links except the one it arrived on.
		• If, however, the broadcast packet arrived on a link other than the preferred one for reaching the source, the packet is discarded as a likely duplicate.
		```

- ## Multicast routing

	- Reverse path forwarding. (a) A network. (b) A sink tree for I. (c) The tree built by reverse path forwarding.
	- slide points
		```
		• Multicasting is a special case of broadcasting
		• All multicasting schemes require some way to create and destroy groups and to identify which routers are members of a group
		• Assume that each group is identified by a multicast address
		and that routers know the groups to which they belong
		• If the group is dense, broadcast is a good start but it reaches
		all routers. The solution is pruning the broadcast tree by
		removing links that do not lead to members
		• If OSPF is used, each routers knows complete topology, they
		can construct its own pruned spanning tree for each sender to the group. Eg. MOSPF (Multicast OSPF)
		```
	- in ip : The **Internet Group Management Protocol (IGMP)** is a communications protocol used by hosts and adjacent routers on IPv4 networks to establish multicast group memberships. IGMP is an integral part of IP multicast and allows the network to direct multicast transmissions only to hosts that have requested them.