# Lecture 31

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/AxVafsH4anI)|

---

- ## Multiclass routing
	```
	• Multicasting is a special case of broadcasting
	• All multicasting schemes require some way to create and
	destroy groups and to identify which routers are members of
	a group
	• Assume that each group is identified by a multicast address
	and that routers know the groups to which they belong
	• If the group is dense, broadcast is a good start but it reaches
	all routers. The solution is pruning the broadcast tree by
	removing links that do not lead to members
	• If OSPF is used, each routers knows complete topology, they
	can construct its own pruned spanning tree for each sender to the group. Eg. MOSPF (Multicast OSPF)
	```
	- class D of ip addresses are reserved for multiclass addresses 
	- IGMP protocol : creating/ managing/ discarding groups when needed/not needed
	
- ## Multicast Routing
	- slide points
	```
	- All of the routers agree on a root (called the **core** or **rendezvous** point) Build the tree by sending a packet from each member to the root
	- The tree is the union of the paths traced by these packets
	- To send to this group, a sender sends a packet to the core
	```
	
- ## Anycast Routing

	- slide points
		```
		• A packet is delivered to the nearest member of a group
		• Can be achieved using regular **DV [Regular Distant Vector]** or **LSR[Link state routing]**
		• All members of the group will be given same address, say 1
		• This procedure works because the routing protocol does not realize that
		there are multiple instances of destination 1. That is, it believes that all the instances of node 1 are the same node
		```
	- ipv4
		- unicast
		- multicast
		- broadcast
	- ipv6	
		- unicast
		- multicast
			- kind of broacast in which all devices are of single group
			- all members of one group
		- anycast
			- deliever of one gruop's any one member
				- to nearest member
		- anycast used when ie resolving address of `google.com` of which servers are located in us and india. accessing google service in india will use india's server which is nearest one.
		
	- contention : fighting for a single resource
	- congestion : traffic
	
- ## Congestion Control Algorithms
	- slide points
	```
	• Approaches to congestion control
		• Traffic-aware routing
		• Admission control
		• Traffic throttling
		• Load shedding
	```

	- redirect packets
	- not new packets admitted | control new packets
	- discard low priority packets
	- traffic throttling -> Redirection
	- load shedding -> dropping some of thee packets
	
	- offered load : given packets
	- goodputs : delivered packets
	
	- When too much traffic is offered, congestion sets in and performance degrades sharply.
	
	- practically 100% goodput is not possible.
	
- ## Approaches to congestion control
	> Slower (preventive) | Open ended service | Planned
	- network provisioning 
		- extra routers in preplanning of network design
		- open loop
	- traffic-aware routing
		- look at current traffic
		- open loop
	- admission control
		- can only be applied in connection oriented 
		- network can reject the new connection
	- traffic throttling
		- traffic redirection
	- load shedding
		- if none of the above method works, then start dropping packets
		- priority field will be used here.
	> Faster (reactive) | Close loop service | not planned applied immediately and get solution
	
	
	- rip is not traffic aware
		- it looks at number of hops
	- ospf is traffic aware