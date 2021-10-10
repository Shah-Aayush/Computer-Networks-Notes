# Lecture 8 *(part 2)*

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=1b352abcbed051064b1241f77c644970) | `iNiZBQp2` |
---

## DataLink Layer
	
- Structure of datalink layer is called **Frame**.
	> A frame is a digital data transmission unit in computer networking and telecommunication. In packet switched systems, a frame is a simple container for a single network packet. In other telecommunications systems, a frame is a repeating structure supporting time-division multiplexing.
	> Sequence of bits
- 0 & +5 are unipolar representation
- -5 & +5 are bipolar representation
- **FSK** : Frequency-shift keying is a frequency modulation scheme in which digital information is transmitted through discrete frequency changes of a carrier signal. : Digital modulation *{Whenever shifting word is used, its called Digital modulation}*
- Datalink layer Design issues
	1. Services offered to network layer
	2. Framing	*{Frame(Header + Packet + Trail)}*
		> Identifying the frame boundry.
	3. Error control
		> Ensuring that frame is not corrupted. Frame integrity is maintained.
		> Checksum and CRC methods are used for ensuring.
	4. Flow control
		> rate control / Speed control
		> i.e. Receiver cannot cop-up with sender's data speed as sender is sending at 10gbps while receiver is able to receive data at 10mbps.
		
### Datalink layer

- Algorithm for achieving :
	- Reliable
	- Efficient communication of a whole units - frames *(as opposed to bits- Physical layer)* b/w two machines
- Two machines are connected by a communication channel that acts conceptually like a wire *(e.g. telephone line, coaxial cable, or wireless channel)*
- Essential property of a channel that makes it **Wire like** *(Ideal channel | Practically impossible)* connection is that the bits are delivered in exactly the same order in which they are sent.
	> less errors in case of fiber optics
- For ideal channel *(No distortion, unlimited bandwidth and no delay)* the3 job of datalink layer be trivial *(unimportant)*
- However, limited bandwidth, distortion and delay makes this job very difficult
	- No distortion : No need of error control
	- unlimited bandwidth : No need of flow control
- Physical layer delivers bits of information to and from data link layer. Thus, functions of data link layer are : 
	1. Providing a well-defined service. interface to the network layer.
	2. Dealing with transmission errors.
	3. Regulating the flow of data so that slow receivers are not swamped by fast senders.
		> Rate control
- Data link layer : 
	- Takes the packets from network layer and
	- Encapsulates them into **frames**
		> `[ Header + Data *{PAYLOAD}* + Tail ]`
	
- Each frame has 
	- **frame header** : fields for holding the packet, and 
	- **frame trailer**
- Frame management is what data link layer does.
	1. Create frame
	2. Transmit frame
	3. Receive frame

- Services provided to the network layer
	- Principal service function of the data link layer is to transfer the data from the network layer on the source machine to the network layer on the destination machine.
		- Process in the network layer hands some bits *(packet)* to the data link layer for transmission.
		- job of data link layer is to transmit the packet to the destination machine so they can be handed over to the network layer process there.