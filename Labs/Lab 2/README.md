# LAB 2

[Watch Video Lecture](https://youtu.be/cBxnASJ7ViI)

- hub is layer 1 device 
	- works at physical layer
	- doesn't understand data layer, network layer
	- cannot read mac address
- switch is layer 2 device
	- maintains switching table/ mac address table 
	- switch learns the mac address 
	- intially target MAC address is set to zeros.
	
- putting one packet in another packet is called encapsulation
- arp is encapsulated in ethernet
- **UDP** : User datagram Protocol
- UDP is put into IP.
- TTL is decreased by one in every router.

- Layer wise protocol which can be determined by wireshark : 
	- Transport layer protocol : UDP
	- Network layer protocol : IPv4
	- Datalink layer protocol : Ethernet 
	
- The bottom section of wireshark is in hexadecimal form.

- Filter types in wireshark 
	1. display filter
		- only specified filters will be displayed which were then on screen.
		- comparision in filter
			- capture packets only which includes *(source/destination)* `10.1.32.5` ip address.
			> `ip.addr == 10.1.32.5`
			- tcp=80
			> `tcp.port==80`
		- **can be applied directly through search bar**
	2. capture filter
		- applied at the time of capturing the packets.
		- i.e. only capture icmp packets.
		- only applied if you are very sure about capturing
 		- can be applied through `capture/select specified option from menu`
			- select the syntax which you need
			- go to `capture/options` paste you syntax in text field. and apply.
			
	- network boundry is called as a hop which is designed by routers. *(not switch)*
	- explore all the commands via running simultanously in wireshark and cmd.
	
- Writing Format
	- AIM :
	- Tools used : 
	- Learning Wireshark :
	- Process : 

- capture user name and password : `http://testphp.vulnweb.com/login.php`