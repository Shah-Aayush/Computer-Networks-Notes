# Lecture 24

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/F0s5HFYr33k)|

---

## DFWMAC - PCF 1


> COMING SOON



## Repeaters, Hubs, Bridges, Switches, Routers & Gateways

- Devices are named according to the layer they process • A bridge or LAN switch operates in the Link layer
- A device will have all below level layer in it including current level layer.
	- like Bridge, Switch : which are datalink layer devices, will also have `Physical Layer` along  with its current Data link layer.
	
	- Application layer : Application gateway
	- Transport layer : Transport gateway 
	- Network layer : Router
	- Data link layer : Bridge, switch 
	- Physical layer : Repeater, hub
	
## VLAN

- IEEE 802.1Q
- in cisco : it's named as `dot 1Q`.
- there should be trunk port in order to connect it with another switch/hub in vlan
- `vlan tag` is there in ethernet.
- priority is a part of 

- Slides : 
	```
	VLANs (Virtual LANs) splits one physical LAN into multiple logical LANs to ease management tasks
	• Ports are “colored” according to their VLAN
	Bridges need to be aware of VLANs to support them
	• In 802.1Q, frames are tagged with their “color”
	• Legacy switches with no tags are supported
	802.1Q frames carry a color tag (VLAN identifier)
	• Length/Type value is 0x8100 for VLAN protocol
	```

- VLAN tagging : 
	```
	- It is placed between the source MAC and the EtherType fields
	- The first two bytes of the tag contain the TPID (tag protocol identifier), which is defined to be equal to 0x8100
	- The remaining two bytes contain the TCI (tag control information), of which 12 bits correspond to the VID and 4 bits contain metadata used for quality of service management.
	```
	- TCI : Tag Control Information : 12 bit VLAN id + 4 bit of meta data
	- priority plays part in quality of service assurance
	
	
	
- VLAN numbering : 
	```
	• Each 802.1Q VLAN is identified by a 12-bit integer called a VID (VLAN Identifier) in the range 1 to 4094 inclusive.
	• The values 0 and 4095 are reserved and should not be used.
	• The first VLAN, with a VID of 1, is the default VLAN to which ports are presumed to belong
	```
	
- VLAN - Ports
	```
	• There are two ways in which a machine can be connected to a switch
	carrying 802.1Q VLAN traffic:
	− via an access port, where VLAN support is handled by the switch (so the machine sees ordinary, untagged Ethernet frames); or
	− via a trunk port, where VLAN support is handled by the attached machine (which sees 802.1Q-tagged Ethernet frames).
	• It is also possible to operate a switch port in a hybrid mode, where it acts as an access port for one VLAN and a trunk port for others (so the attached Ethernet segment carries a mixture of tagged and untagged frames)	
	```

- Auto trunk
	- not advisable as it opens for hackers to attack system via connecting it to trunk mode or other and stealing information. (*security concerns*)
	