# Lecture 9

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=7eda1536fbfafd7a34a711bb10c32694) | `CtJBHKH6` |
---

- Possible services offered
	- Unacknowledged connectionless service
		- It consists of having the source machine send independent frames to the destination machine without having the destination machine acknowledge them.
		- In all the communication channel where real time operation is more important than quality of transmission.
		- Example : Ethernet, Voice over IP etc.
		> No reliability guarantee
		> Timely delivery of packet is important.
		> No delay
		> No retransmission
		> Live streaming
	- Acknowledged connectionless service
		- Each frame sent by the data link layer is acknowledged and the sender knows if a specific frame has been received or lost.
		- Typically the protocol uses a specific time period that is has passed without getting acknowledgment it will re-send the frame.
		- This service is useful for communication when an unreliable channel is being utilized. (e.g. : 802.11 WIFI)
		> Compared to wired network, <u>wireless network is always unreliable</u>
	- Acknowledged connection-oriented service
		> there will not be an unacknowledged connection-oriented service.
		- Source and destination establish a connection first.
			> For making connection, we need to send **Control packet** first. it will go to other side for making connection.
		- Each frame is numbered
			- Data link layer guarantees that each frame send is indeed received
			- It guarantees that each frame is received only once and that all frames are received in the correct order.
		- Example : 
			- Satellite channel communication.
		- For acknowledged service, we have to do a *sequence numbers*.
		- Time required by the packet to go from sender to receiver is called as **Propagation delay**.
		- Going from sender to receiver and coming back to sender is called **RTT : {Round Trip Time}**.
			- `B - Bytes`
			- `b - bits`
		- **Transmission time** : the transmission time is the amount of time from the beginning until the end of a message transmission. In the case of a digital message, it is the time from the first bit until the last bit of a message has left the transmitting node.
		- **Bandwidth/Datarates** : Bandwidth is the data transfer capacity of a computer network in bits per second (Bps). The term may also be used colloquially to indicate a person's capacity for tasks or deep thoughts at a point in time.
		```math
		- Transmission time = Frame size / Bandwidth
		```
		
- Example : 
	``
	Frame length = 1000 byte
	DataRate/Bandwidth = 1 mBps
	Transmission time : FL/DR = 10^3/10^6 = 10^-3 sec
	Propogation time : 3 sec
	RTP : 6 sec
	When another frame is loading, the time after : 6.001 sec *{0.001 secs for transmission + 6 secs for travelling + assuming acknowledgement time is ZERO}*
	Effective data rate you could achieve : 1000/6 bytes/second [1000 bytes per 6 seconds so 1000/6 bytes per second : *Data transmitted in this 6 seconds*]
	Efficiency : 166/10^6 *Efficiency will be 100% here when we send 10^6 bytes per second. but here we can only send 166.6 data per second so it will be too low :( | This is NOT ACCEPTABLE*
	``
	- This is **STOP AND WAIT PROTOCOL** 
	- Very low efficiency

- Every frame has to be number when we don't want to stop and wait and want to continuously sending ACKs.
	> ACKs will carry the frame number so that sender can know.

## Framing
- Three distinct phases : *[Connection oriented]*
	1. Connection is established by having both side initialize variables and counters needed to keep track of which frames have been received and which ones have not.
	2. One or more frames are transmitted
	3. Finally, the connection is released - freeing up the variables, buffers, and other resources used to maintain connection.

	> some kind of variables, timers, buffer memory and counters required here.

- Physical layer talks about bit layer, signal layer. it will not think about frame level.

- To provide service to the network layer, the data link layer must use the service provided to it by physical layer.
- Stream of data bits provide to data link layer is not guaranteed to be without errors.
- Errors could be : 
	- Number of received bits does not match number of transmitted bits *(deletion or insertion)*
	- Alternation of bit value
- It is up to data link layer to correct the errors if necessary
- Transmission of data link layer starts with breaking up the bit stream
	- into discrete frames
	- Computation of a checksum for each frame, and 
	- Include the checksum into the frame before it is transmitted
- Receiver computes its checksum error for a receiving frame and if is different from the checksum that is being transmitted will have to deal with error.
- Framing is more difficult than one could think!

## Framing methods
- Byte counts
	- It uses a field in the header to specify the number of bytes in the frame
	- Once the header information is being received it will be used to determine end of the frame.
	- trouble with this algorithm is that when the count is incorrectly received the destination will get out of synch with transmission.
		- destination may be able to detect that the frame is in error but it does not have a means *(in this algorithm)* how to correct it.
- Flag bytes with byte stuffing
	- This methods gets around the boundary detection of the frame by having each frame appended by the start and end special bytes.
	- if they are the same *(beginning and ending byte in the frame)* they are called **Flag byte**.
	- If the actual data contains a byte that is identical to the **FLAG** byte *(e.g. picture, data stream etc.)* the convention that can be used is to have escape character inserted just before the *FLAG* character.
> <u>*{Lecture 10 starts from here...}*</u>
- Flag bits with bit stuffing	
	- This methods achieves the same thing as Byte stuffing method by using Bits *(1)* instead of Bytes *(8 bits)*
	- It was developed for high-level data link control *(HDLC)* protocol.
	- Each frames begins and ends with a special bit pattern : 
		- `01111110` or `0x7E` <- Flag Byte		*{In message; not in headers/tailors}*
		- Whenever the sender's data link layer encounters five consecutive 1s in the data it automatically stuffs a 0 bit into the outgoing bit stream
		- USB uses bit stuffing
- Physical layer coding violations.
	- Violating Physical Layer encoding : 
		- Many networks uses encoding techniques like Manchester, differential Manchester encoding.
			- **Differential Manchester encoding** is a line code in digital frequency modulation in which data and clock signals are combined to form a single two-level self-synchronizing data stream.
			- **Manchester code** is a line code in which the encoding of each data bit is either low then high, or high then low, for equal time. It is a self-clocking signal with no DC component. Consequently, electrical connections using a Manchester code are easily galvanically isolated.
			> Every bit in manchester and differential manchester encoding has high-low & Low-high pairs
		- These techniques have transition in middle of each bit.
		- Violating this and using a high-high or low-low pair of indicating beginning or end of frame.