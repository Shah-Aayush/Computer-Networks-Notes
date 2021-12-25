# Lecture 23

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/F0s5HFYr33k)|

---

- IFS : Inter Frame Space
	- Spacing b/w two frames

- In ethernet there is no ACK. but in wireless there is.
	- ACK are very short compared to a dataframe
	
- B/w any two frame there will be some gape called IFS
- gape means there will be free medium and there will be no activity.

- Polling response : 
	- PS : Power Save poll packet

- MAC layer 2
	```
	Priorities
	• defined through different inter frame spaces
	• no guaranteed, hard priorities
	• SIFS (Short Inter Frame Spacing)
	− highest priority, for ACK, CTS, polling response • PIFS (PCF IFS)
	− medium priority, for time-bounded service using PCF • DIFS (DCF, Distributed Coordination Function IFS)
	−
	lowest priority, for asynchronous data service
	```
	
- Priority : **SIFS>PIFS>DIFS**

- Fairness is an issue with the ethernet but not in case of wireless.

- CSMA/CA access method 1
	```
	• station ready to send starts sensing the medium (Carrier Sense based on CCA, Clear Channel Assessment)
	• if the medium is free for the duration of an Inter-Frame Space (IFS), the station can start sending (IFS depends on service type)
	• if the medium is busy, the station has to wait for a free IFS, then the station must additionally wait a random back-off time (collision avoidance, multiple of slot-time)
	• if another station occupies the medium during the back-off time of the station, the back-off timer stops (fairness)
	```

- Duration  : Random number generated * 50 micro seconds

- If any two frame's random number or backoff interval is same then they will collide.

- Only hidden node problem is solved by RTS-CTS. Exposed node problem is not yet solved.

- RTS has field Duration which tells the required time to complete whole transaction.

- CSMA/CA access method I
	```
	Sending unicast packets
	- station has to wait for DIFS before sending data
	- receivers acknowledge at once (after waiting for SIFS) if the packet was received correctly (CRC)
	- automatic retransmission of data packets in case of transmission errors
	```

- DFWMAC method II
	```
	Sending unicast packets
	• station can send RTS with reservation parameter after waiting for DIFS (reservation determines amount of time the data packet needs the medium)
	• acknowledgement via CTS after SIFS by receiver (if ready to receive)
	• sender can now send data at once, acknowledgement via ACK
	• other stations store medium reservations distributed via RTS and CTS
	```

- Duration field in RTS will include time from `SIFS-CTS` to `SIFS-ACK`. which means : `3*SIFS + CTS + Data + ACK`

- NAV : Network Allocation Vector.
	- its a counter for which the point will not transmit the data or doesn't interfere on current on going transmission.
	- Virtual career sensing. medium will be busy for them.
	
- Fragmentation
	- If there are multiple frames, we should do all at once i.e. content once, transmit all the fragments.
	- The duration field in fragment one will contain the time for next packet

- PCF : (Point coordination function)
	- **Centralized.**