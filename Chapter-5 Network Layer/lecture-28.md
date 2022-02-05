# Lecture 28

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/IiU-HaTfLE4)|

---

routing : continuesly running on background; mainting routing table
forwarding : per packet base execution; see the destination ip add; refer routing table;  figure out path; next hop decision


- ## Routing Algorithms
	```
	Desirable properties of routing algorithm: 
	Correctness – Right path is chosen 
	Simplicity – Ease of use and implementation 
	Robustness – reliability in event of failure 
	Stability - converge to fixed set of paths 
		> after some time, routing table should be stable
	Fairness – Fair to all hosts
	Efficiency – Utilization, delay, throughput
		>  througput : the amount of data moved successfully from one place to another in a given time period
	```

- ## Fairness vs. Efficiency
	- fairness : A,B,C should get similar number of time/chance  to tranmit
	- have to stop A,B,C  , if X wants to transmit.
	- sometimes we have to sacrifice fairness in order to acheive efficiency.
	
- ## Types of routing algorithms
	- **Nonadaptive RA** – do not base their routing decisions on any measurements or estimates of the current topology and traffic. Instead the routes are computed in advance, offline and downloaded to routers when network boots. Eg <u>Static Routing</u>
		> not dynamic
	- **Adaptive RA** - change their routing decisions to reflect changes in the topology, and sometimes changes in the traffic as well. They differ in where they get their information, when they change the routes, and what metric is used for optimization. Eg <u>Distance Vector Routing</u>, <u>Link State Routing</u> 
		- *[Link State Routing: OSPF : update routing table based on current traffic : composite metric (delay, throughput, number of hop)]*
		- *[Distance vector routing : RIP : Routing Information Protocol : counts number of hops. : every 30 secs updates routing table]*
		> dynamic
	
- ## The Optimality Principle
	- Statement about optimal routes without regard to network topology or traffic
	- It states that if router J is on the optimal path from router I to router K, then the optimal path from J to K also falls along the same route.
	- Otpimal path is concatination of several optimal subpaths
	
	
	- a sink tree which is transformed from network always has a root router.
	- trees are logical paths.
	- making tree for every node will generate routing paths /table
	
- ## Flooding
	```
	A simple method to send a packet to all network nodes
	Each node floods a new packet received on an incoming link by sending it out all of the other links
	Flooding generates vast numbers of duplicate packets, in fact, an infinite number unless some measures are taken to damp the process.
	One such measure is to have a hop counter contained in the header of each packet that is decremented at each hop.
	The packet being discarded when the counter reaches zero.
	Ideally, the hop counter should be initialized to the length of the path from source to destination.
	If the sender does not know how long the path is, it can initialize the counter to the worst case i.e. the full diameter of the network.
	First, it ensures that a packet is delivered to every node in the network.
	This may be wasteful if there is a single destination that needs the packet,
	but it is effective for broadcasting information.
	flooding will find a path if one exists, to get a packet to its destination(e.g. in a military network located in a war zone).
	```
	
	- Flooding vs Broadcasting
		- broadcast is not a way of forwarding a packet. it's a way of delivering the packet.
		- to whom to deliver is the task of broadcast.
		- every computer will receive and process the packet in broadcasting.
		
		- forwarding a packet in all direction (except the one from where it was received) because node doesn't know to which node it should forward. this is called **FLOODING**.
			- if router doesn't know the destination, then it will work like a hub. | using flooding.
		- not every computer will receive and process. 
		- kind of routing protocol.
		
		- problems with flooding : 
			- bandwidth wastage
			- lot of packet/ many copies generated
			
		- solution : 
			- maintain sequence number | help to control the flood.
			- set the age of the packet. | ttl - time to leave type concept. *like in ip*
		
	
- ## Shortest path algorithm
	- need to have complete network graph available on every node in order to run this algorithm.
	- create label for every node except root node
	- solid node/network : permanant 
	- transient/temporary : hollow bubble/network node
	
	
	1. in starting all the nodes are transient
	2. identify label with the smallest value
		- make it solid bubble
			- make it permanent
		- make it current node
			- points arrow to that node
	3. update label of all neighbours of b
		- figure out smallest label and make it current, solid node
	4. update label of current node
	
	> ITERATIVE PROCESS until reaches the destination
	
	-  code
		```c
		# define MAX_NODES 1024 				/* maximum number of nodes */ 
		# detine INFINITY 1000000000 			/* a number larger than every maximum path */
		int n, dist[MAX_NODES][MAX_NODES]		/*dist[i][j] is the distance from i to j*/ 
		void shortest_path(int s, int t, int path[])
		{ 
			struct state { 						/* the path being worked on */
				int predecessor; 				/* previous node */
				int length; 					/* length from source to this node */
				enum {permanent, tentative} label; 	/* label state */
			} state[MAX_NODES]; 
			int i, k, min; 
			struct state *p; 
			
		for (p = &state[0]; p < &state[n]; p++) { /* initialize state */ 
			p->predecessor = —1; 
			p->length = INFINITY; 
			p->label = tentative; 
		}
		state[t].length = 0; 
		state[t].label = permanent; 
		k = t; /* k is the initial working node */ 
		do { /* Is there a better path from k? */ 
			for (i = 0; i < n; i++) /* this graph has n nodes */ 
				if (dist[k][i] != 0 && state[i].label == tentative) {
					if (state[k].length + dist(k][iJ < state[i].length){
						state[i].predecessor = k; 
						state[i].length = state[k].length + dist[k][i]; 
					}
				}
				/* Find the tentatively labeled node with the smallest label. */ 
				k = 0; min = INFINITY; 
				for (i = 0; i < n; i++) 
					if (state[i].label == tentative && state[i].length < min) { 
						min = state[i].length; 
						k = i; 
						state[k].label = permanent; 
					}
		} while (k != s); 
		/* Copy the path into the output array. */ 
		i = 0; k=s; 
		do {path[i++] = k; k = state[k].predecessor; } while (k >= 0); 

		}
		```