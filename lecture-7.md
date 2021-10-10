# Lecture 7

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=34cc4f628a9186300ea58ee1007e577b) | `rWyY4mES` |
---

- Any protocol running at any specific layer is a protocol between that entity and the immediately next entity network layer.
- **Gateway** : A gateway is a network node used in telecommunications that connects two networks with different transmission protocols together. Gateways serve as an entry and exit point for a network as all data must pass through or communicate with the gateway prior to being routed.
	> Email and SMS gateway are application layer protocols. 
	> Sending SMS through website, involves HTTP at sender side and STP at receiver side. in b/w there is a gateway. In this way, an HTTP packet will be converted to SMS packet. used for send different type of packet to one application layer to another application layer protocol.
	> This gateway is intermediate device
	> SMS gateway is works at application layer./ Transport layer
	
- OSI model : *Jobs of layers*
	1. Application : 
		> **Simple Network Management Protocol** (SNMP) is a networking protocol used for the management and monitoring of network-connected devices in Internet Protocol networks.
		> HTTP, SMP likewise protocols...
		> Interacting with the user

	2. Presentation : meaning of the information should not change over network
		> ASN : Abstract Syntax Notation
		> to preserve the meaning
		> EBCDIC coding : Extended Binary Coded Decimal Interchange Code 
	3. Session : session management, check-pointing *{resumes download}*
	4. Transport : End to end protocols *{b/w 2 hosts}*
	5. Network : Network management, {2 different networks means another router included}, congestion control, routing, quality of service
		> Downloading file at variable speed doesn't affect the after downloaded file. *this is quality of service*
		
	|YouTube Video streaming| Downloading file|
	|--|--|
	|Delay should be less| Reliability should be more|
	|Its okay if packet is dropped but should not be late|Its okay if packet is late but should not drop|
	
	6. Data link : (encryption in Wifi ) error control, framing, flow control, Link management
	7. Physical : responsible for multiplex, demultiplexing, channel coding, spreading-despreading
	
	
- TCP/IP reference model layers
	- Link layer *{Datalink layer + Physical layer}*
	- Internet layer	*{Network layer}*
	- Transport layer
	- Application layer *{Merged all remaining layers in this : Application + Presentation + Session }*
	
- TCP/IP ref models : 
	> The tcp/ip ref model with some protocols
	Protocols : 
		- Application : `HTTP`, `SMTP`, `RTP`, `DNS`
		- Transport : `TCP`, `UDP`
		- Internet : `IP`, `ICMP`
			> ICMP is helper protocol to IP
			> ICMP is not full-fledged network protocol. but its support protocol of IP.
		- Link : `DSL`, `SONET`, `802.11`, `Ethernet`

- Hybrid reference model which we will  be using  :
	5 Application
	4 Transport
	3 Network
	2 Link
	1 Physical
	
- OSI : only was Theoretical *(Reference model)*
	> there was no implementation
	
-  Example networks :
	1. Internet
	2. ARPANET
		> **IMP** : The Interface Message Processor was the packet switching node used to interconnect participant networks to the ARPANET from the late 1960s to 1989. It was the first generation of gateways, which are known today as routers. 
	3. NSFNET		*[Not covered in this course]*
	4. Third-generation mobile phone networks		*[Not covered in this course]*
	5. RFID and sensor networks		*[Not covered in this course]*