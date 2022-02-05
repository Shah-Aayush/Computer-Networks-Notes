# Lecture 29

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/HX34D2GoZRk)|

---

<!-- whats special in this lecture? => Oh c'mon hAnsh! 😂 (One of my friend ANSH caught by vijaysir for joining late in the lecture and his excuse was hilarious 😆🙌 ) -->

- ## Flooding
	- kind of routing protocol
	- can decide where to forward packet
		- which nodes will be receiving
	- like HUB
	- forwarding the packet
	
- ## Broadcast
	- delivery mechanism
	- like unicast, multicast, anycast
	- decides which stations will receive
	- receiving and processing the packet
	
- ## Distance Vector Routing
	- Table generated is called Distance Vector
	- third column is [origin of the vector] is not included in the next tranmission of routing table forwarding of `J`
	- How `J` will reach the given destination will not be revealed. only cost will be revealed.
	
- ## The Count-to-Infinity Problem 
	- after millions of exchanges, if one link breaks the other link will falsly believe the path and  keep on increasing... at the end it will become INFINITY
	> *GOOD NEWS SPREADS PROPERLY. Distant Vector doesn't perform well for BAD NEWS.*

	- SOLUTION TO THIS PROBLEM : 
		- Split horizon (hack)
		- Poison reverse
	
	- Distant vector is a concept. actual implementation is **RIP**.

- ## Link State Routing
	- Conceptual routing
	- not an implementation
	- OSPF | open shortest path first
	
	```
	• Discover neighbors, learn network addresses. | measured by first `hello` packet
	• Set distance/cost metric to each neighbor.
	• Construct packet telling all learned. | only neighbours information is carried.
	• Send packet to, receive packets from other routers. | flooding
	• Compute shortest path to every other router.  |  dijkstra's algo applied
	```
	
	