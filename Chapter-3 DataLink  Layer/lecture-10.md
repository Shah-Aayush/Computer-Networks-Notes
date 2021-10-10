# Lecture 10

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=8b883bce515ad48230027bc060f5cbd4) | `Jk4sGSX6` |
---

## Error control

- After solving the marking of the frame with start and end the data link layer has to handle eventual errors in transmission or detection.
	- Ensuring that all frames are delivered to the network layer at the destination and in proper order
- For unacknowledged connectionless service : it is *OK* for the sender to output frames regardless of its reception
	> Here its okay if we ignore the error control.
- For reliable connection-oriented service : it is *NOT OK*.
	> Here error control problem is to be solved.
- Reliable connection-oriented service usually will provide a sender with some feedback about what is happening at the other end of the line.
	- Receiver sends back special control frames. *(control frame is ACKs only!)*
	- if the sender receives positive acknowledgement it will know that the frame has arrived safely.
- Timer and frame sequence number for the sender is necessary to handle the case when there is no response *(Positive or Negative)* from the receiver.
	
## Flow control 
- Important design issue for the cases when the sender is running on a fast powerful computer and receiver is running on a slow low-end machine.
- Three approaches : 
	1. Feedback-based flow control
		- Receiver sends back information to the sender giving it permission to send more data, or
		- Telling sender how receiver is doing.
			> capability of receiver
		- Most data link layer protocols uses feedback based flow control.
		> **STOP & WAIT**
	2. Rate-based flow control
		- Built-in mechanism that limits the rate at which sender may transmit data, without the need for feedback form the receiver.
		- ABR *(Available Bit Rate)* service in ATM *(Asynchronous Transfer Mode)* uses rate-based flow control
			> **Available bit rate (ABR)** is a service used in ATM networks when source and destination don't need to be synchronized. ABR does not guarantee against delay or data loss. ABR mechanisms allow the network to allocate the available bandwidth fairly over the present ABR sources.
			> **Asynchronous Transfer Mode (ATM)** is a telecommunications standard defined by ANSI and ITU for digital transmission of multiple types of traffic, including telephony, data, and video signals in one network without the use of separate overlay network
		- Just calculate the max rate at which data can be received or send. and then don't exceed that rate limit! 
	3. Credit-based flow control
		- sender is given explicit credit by the receiver. Utilize the credits on each byte. Transmit at any rate till the credits are available. Pause when the credits are over and wait for more credits to come.
		- TCP implements credit based flow control.
		- No speed limit here. but content limit is there *(of credit)*.
- Fast computers should not dominate over the slow computers.

## Error detection and Correction

- Two basic strategies to deal with errors : 
	1. Include enough redundant information to enable the receiver to deduce what the transmitted data must have been. 
		> **Error correcting codes**
		> Sending extra data with our original data which is redundant bits. (extra bits which doesn't carry the information)
	2. Include just enough redundancy to allow the receiver to deduce that an error has occurred *(but not which error)*
		> **Error detecting codes**
- Receiver can correct the code without help of sender / retransmission with error correction.
- Error codes are examined in Link Layer because this is the first place that we have run up against the problem of reliably transmitting groups of bits.
- Error codes have been developed after long fundamental research conducted in mathematics.
- Many protocol standards get codes from the large field in mathematics.
- All the codes add redundancy to the information that is being sent. 
- A frame consists of m data bits (message) and r redundant bits (check). 
- n total length of a block (i.e., n = m + r) 
- n bit codeword containing n bits. 
- (n, m) code 
- m/n code rate (range '/2 for noisy channel and close to 1 for high-quality channel). 

- Number of bit positions in which two codewords differ is called **Hamming Distance**. It shows that two codes are d distance apart, and it will require d errors to convert one into the other. 
	- Correction capability : 
		> To correct `1` bit error, we need at least `3` bit of hamming distance
		> To correct `2` bit error, we need at least `5` bit of hamming distance
		> To correct `D` bit error, we need at least `2D+1` bit of hamming distance
	- Detect capability : 
		> To detect `D` bit error, we need at least `D+1` bit of hamming distance
- Example : 
	- Transmitted: `10001001` 
	- Received: `10110001` 
	- XOR operation gives number of bits that are different. 
	- XOR: `00111000` 
	> HAMMING DISTANCE IS **3** here.
- **Block coding** refers to the technique of adding extra bits to a digital word in order to improve the reliability of transmission.

- All 2^m possible data messages are legal, but due to the way the check bits are computed not all 2n possible code words are used. 
- Only small fraction of 2^m/2^n= 1 /2^r will be legal codewords. 
- The error-detecting and error-correcting codes of the block code depend on this Hamming distance. 
- To reliably detect d error, one would need a distance d+1 code. 
- To correct d error, one would need a distance 2d+1 code. 

- Example: 
	- 4 valid codes: 
		— 0000000000 
		— 0000011111 
		— 1111100000 
		— 1111111111 
		> **This code has hamming distance of 5 so that it can detect `4 bit` of error and can correct `2 bit` of error.**
	- Minimal Distance of this code is 5 => can correct double 
	errors and it detect quadruple errors. 
	- 0000000111 => single or double — bit error. Hence the receiving end must assume the original transmission was 0000011111. 
	- 0000000000 => had triple error that was received as 
	0000000111 it would be detected in error. 

- Error correction vs Error detection

	|Correction| Detection|
	|--|--|
	|high Redundancy | Less redundancy|
	|Less overhead | high overhead (as retransmission is there ) | 

- **the bit error rate (BER)** : is the percentage of bits that have errors relative to the total number of bits received in a transmission, usually expressed as ten to a negative power
	> Fiber optic : 10^-17		{Less error chances}
	> Wifi : 10^-3		{More error chances}
	- `EXAMPLE` : If a frame is of length 1000 bits. suppose it is wireless medium and its BER is 10^-3. so that it means out of 1000 bits, 1 bit will be corrupted. so if we use error detection technique here, it will be useless. because it will tell at every frame that the frame is corrupted and it should be retransmitted because the frame length is 1000 bits and 1 bit of it will always be corrupted. in this case we should use **ERROR CORRECTION TECHNIQUE**
	
	
## HAMMING CODE, CRC, Checksum
> Refer this part from pdf.

- One cannot perform double error correction and at the same time detect quadruple errors. 
- Error correction requires evaluation of each candidate codeword which may be time 
	consuming search. 
- Through design this search time can be minimized. 
- In theory if n = m + r, this requirement becomes: (m + r + 1)<= 2^r 
- Codeword: bl b2 b3 b4 .... 
- Check bits: The bit positions that are powers of 2 (p1, p2, p4, p8, p16, ...). 
- The rest of bits (m3, m5, m6, m7, m9, ...) are filled with m data bits. 
- Example of the Hamming code with m = 7 data bits and r = 4 check bits is given in the next slide. 
