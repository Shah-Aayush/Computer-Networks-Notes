# Lecture 6

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=fde9e1714902f405131e0cef896cfac7) | `dWmFM5vU` |
---

- Reference models
	- OSI ref model
	- TCP/IP ref model
	- Model used for this text
	- Comparison of OSI and TCP/IP
	- Critique of OSI model and protocols
	- Critique of TCP/IP model
	
- OSI ref model 
	- Layers created for different abstractions
	- Each layer  performs well-defined function
	- Function of layer chosen with  definition of international standard protocols in mind.
		- Web transfer : HTTP
		- File transfer : FTP
		- Email : SMTP
	- Minimize information flow across interfaces
		- Communication should be minimum between two consecutive layers
		- **Loose coupling** means that the degree of dependency between two components is very low. **Tight coupling** means that the degree of dependency between two components is very high.
		- Here we accept *loosely coupled* system.
		- Changing one protocol in one layer should not affect the other layers.
	- Number of layers should be optimum {5-6-7 layers should be resonable}
	
- Modularization : 
	> any module can call other module as per requirement
	1. Component based modularization
	2. Layered modularization {strictly layer based communication}

- OSI model :
	1. Application
	2. Presentation
	3. Session
	4. Transport
	5. Network 
	6. Data link
	7. Physical 

- Two computers in different networks can only be connected using a **router**. cannot use a hub or switch.
- At network layer, routers works.
- physical, data link and network layers are there in routers.
	- Routers are at network layers. [layer 3 device]
	- Hosts are at Application layers.
	- Switch are at Datalink layers. [layer 2 device]
	- Repeaters and hubs are at physical layers. [layer 1 device]
- Peer protocol is always immediately next same protocol layer. Like in two different networks' computers which are connected through two routers in between, The 1st computer's physical layers's peer is immediately next physical layer of router 1. 
	> so if we are using ethernet as 1st computer's physical layer, we must use ethernet at router 1's physical layer. the destination   computer's layer, we can use wifi! but not at router 1. There can be different things b/w two routers. but there must be similarity  b/w router and its connected host.
- Transport layer *{and its above layers}* is host to host protocol	*[End to end protocol]*
- Network layer is host to router protocol
