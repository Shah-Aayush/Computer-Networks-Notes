# LAB 1

[Watch Video Lecture](https://youtu.be/u4w2ggDq39c)

# network commands

- `ping` 
	- request message send to target computer.
	- packet sent to target message.
	- if target computer receives packet it should respond.
	- total 4 responses generated generally in windows while in linux, it generates infinite requests until we end the process.
	- ping is not a protocol
	- but protocol used by ping is `ICMP`.
	- icmp response are received by it.
	- `bytes` are payload of the packet
	- `time` how much time take reply tranmission.
	- `ttl` time to leave , age of the packet, ttl=5 means packet can travel upto 5 hops *(network boundry)*
	- at every router, network changes. i.e. in nirma campus, if we access nirma website then it will travel 0 hops as server is located in nirma itself. but if we ping `google.com` then it will travel many hops through which network changes.
	- continues `ping` on **windows** : `ping <ip-address> -t`
	- all possible diffrent ways of using `ping` : `ping /?` *(Windows)* or `ping` *(MacOS)*
	- **Use ping command to know all the hops to `google.com`**
		> `-r count`
		> `pathping google.com`
		- Displays the IP addresses of the hops taken along the route to the destination. Specify a number between 1 and 9. If the number of actual hops exceeds the number you specify, you will get a "Request timed out" message.

		> `-s count`
		- Displays a timestamp for the Echo Request and the Echo Reply Request for hops along the route. Specify a number between 1 and 4. If the number of actual hops exceeds the number you specify, you will get a "Request timed out" message.
	- [best resource : read more...](https://www.csie.ntu.edu.tw/~b90047/ebook/winXPhack/0596005113_winxphks-chp-5-sect-12.html)
	
- `ipconfig`
	- `ifconfig` for macos
	- ip address of the current pc,  mac address like information is displayed.
- `netstat`
	- network statastics
	- all  the active connection from my pc to other pcs and networks
	- ip address:port number
	- connection is always between two processes. not b/w two computers. 
	- process is identified by port number and computer is identified by ip address.
	- `CLOSE_WAIT` : waiting for the connection to close.
	- we can see the hidden malicious activity from this command.
	- `netstat -r` : routing table of the current pc.
- `traceroute`
	- for windows : `tracert`
	- for macos : `traceroute`
	- displays path to destination network
- `nslookup`
	- ns : `name server`
	- dns : domain name server
	- host's ip address is stored on a dns server.
	- `google.com` is a domain name.
	- will return `DNS` server address.
	- ipv6 is in Hexadecimal number *(colon notation)*
	- ipv4 is in dotted decimal
	- domain name : application layer address
	- ip address : network layer address
	- port number : used to identified process
	- mac address/ethernet : physical address : 48 bit:  represented in hexadecimal  : used within LAN.
	
	
- `finger`
	- related process
	- Finger command is a user information lookup command which gives details of all the users logged in. This tool is generally used by system administrators. It provides details like login name, user name, idle time, login time, and in some cases their email address even.

- `fping`
	- fping is a small command line tool to send ICMP (Internet Control Message Protocol) echo request to network hosts, similar to ping, but much higher performing when pinging multiple hosts.

- `Arp`
	- the table which maintain the mapping b/w ip and mac address is called ARP table.	
	- `arp -a`
	- Address Resolution Protocol

- subnet mask in nirma : 255.255.0.0
	- dotted decimal notation
	- `10` is first octet here

- 