# Lecture 5

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=0beda92c09dcc166f56745c5f9af15f2) | `BvxFBhQ3` |
---

- Network software
	- Protocol Hierarchies
		> Protocols are softwares.
	- Design issues for the layers
	- Connection-oriented versus connectionless service
		> Datagram is connection less and Virtual Circuit is connection oriented.
	- Service primitives
	- Relationship of services to protocols
	
- OSI has 7 layers
- TCP/IP has primary 5 layers
- Layers in protocols are not fixed. it can be anything. Layers works same like functions in C language
	>Agreement b/w two parties *{PROTOCOLS}*
	- HTTP : Layer 5 protocol : application layer
		- Both sides should have same protocols at respective layers.
	- TCP : Layer 4 protocol : for Security 
	- IP : Layer 3 protocol : Manage network  :routing, quality control, congestion control
	- xyz : Layer 2 protocol : Data link layer
	- Ethernet : Layer 1 protocol : Physical layer
		> Modulation done here
		> Demodulation will be done another side

- Communications happens b/w two layers using **interfaces**
	> Method only without definition
	> For passing packet from layer 5 to layer 4, layer 5 will call the function of layer 4.
- <u>This is hierarchy of protocols; Strict sequence to be followed. </u>
_Extra information can be added at every layer_

> Splitting long-a** messages into smaller parts is called **Fragmentation**. This can be reassembled at other side*

- Header and trailer both can be there in layer 2 
	> *{trailer may be, may  not be added !}*
- **Checksums :** A checksum is a value that represents the number of bits in a transmission message and is used by IT professionals to detect high-level errors within data transmissions. Prior to transmission, every piece of data or file can be assigned a checksum value after running a cryptographic hash function.
	> Checksums can be added at trailer.
	> Miss-match in checksums can lead to errors and that packet should be retransmitted.

- **Connection Oriented service** vs. **Connection less service**
	> Six different types of service
	
	|Type|Service|Example|
	|--|--|--|
	|Connection oriented |Reliable message stream | Sequence of pages|
	|Connection oriented |Reliable byte stream | Movie download|
	|Connection oriented |UnReliable connection (no NEVER retransmission)| voice over ip (whatsapp call or anything like that : Loss of any one packet will not be retransmitted)|
	|Connection less |UnReliable datagram (i.g. ip transmission)| Electronic junk mail|
	|Connection less |Acknowledged datagram |Text messaging|
	|Connection less |Request-reply | Database query|
	
	
	> Service primitives : Six service primitives that provide a simple connection-oriented service
		- Layer 3 is providing service to layer 4 for routing
		- So lower layer is always stay  to offer certain services to upper layer.
		- Upper layer are service user of lower layer
		- Service is kind of facility 
		- The way you access services is called **servicePRIMITIVES**
|Primitive|Meaning|
|--|--|
| Listen | Block waiting for an incoming connection |
| Connect | Establish a connection with a waiting peer|
| Accept | Accept an incoming connection from a peer |
| Receive | Block waiting for an incoming messasge|
| Send | Send a message to the peer |
| Disconnect | Terminate a connection |