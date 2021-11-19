# Lecture 12

|Watch Video Lecture|
|---|
|[youtube link](https://youtu.be/FVUhgVlLGas)|

| Video Lecture | Password |
|--|--|
| [Lecture link](https://nirmauni.webex.com/nirmauni/ldr.php?RCID=c1803cdf1c2c7e32a5ae4ffa808405da) | `jK4kfkid` |
---
	
- **Protocol.h file :**
	
	```c
	#define MAX_PKT 1024                    /* packet size in bytes */
	
	typedef enum { false, true } boolean;   /* boolean type */
	typedef unsigned int seq_nr;            /* sequence or ACK numbers */
	
	typedef struct {
	unsigned char data[MAX_PKT];
	} packet;                               /* packet definition (Payload field) */
	typedef enum { data, ack, nak } frame_kind; /* frame kind definition (Three types of frames : data frame {sender sends to receiver}; ACK frame {receiver sends positive ACKs to sender}; NAKs {receiver sends negative ACKs to sender}) */
	
	
	typedef struct {
	frame_kind kind;                    /* what kind of frame? */
	seq_nr seq;                         /* sequence number (of data frame)*/
	seq_nr ack;                         /* ACK number */
	packet info;                        /* the Network layer packet (Payload field) */
	} frame;
	
	/* final packet block : [kind | seq | ack | info]*/
	
	/* wait for an event to happen; return its type of event  (event can be like packet arrival, packet loss etc.)*/
	void wait_for_event(event_type *event);
	
	/* fetch a packet from the network layer for transmission */
	void from_network_layer(packet *p);		//(take something from network layer)
	
	/* deliver information from an inbound frame to the network layer (this functions needs on receiver side)*/
	void to_network_layer(packet *p); //(give something to network layer)
	
	/* get an inbound frame from the physical layer (receiver side)*/
	void from_physical_layer(frame *r);
	
	/* pass the frame to the physical layer */
	void to_physical_layer(frame *s);
	
	/* start the clock and enable the timeout event */
	void start_timer(seq_nr k);		// (for every frame we have to start timer || SENDER SIDE)
	
	/* stop the clock and disable the timeout event */
	void stop_timer(seq_nr k);		// (if ack is received before timer interval so we can stop timer. || SENDER SIDE)
	
	/* start an auxiliary timer and enable the ack_timeout event */
	void start_ack_timer(seq_nr k);		// (of less time interval then above timer. || RECEIVER SIDE || Acks generating time)
	
	/* stop an auxiliary timer and disable the ack_timeout event */
	void stop_ack_timer(seq_nr k);		// (RECEIVER SIDE)
	
	/* allow the network to cause a network_layer_ready event */
	void enable_network_layer(void);
	
	/* forbid the network to cause a network_layer_ready event */
	void disable_network_layer(void);
	
	/* macro inc */
	#define inc(k) if (k < MAX_SEQ) k = k + 1; else k = 0
	```

- **Utopian Simplex protocol 1**

	- There are certain assumptions here : 
		- No flow control is required here.
		- Simplex 
		- No error control is required.

	```c
	/* Protocol 1 (utopia) provides for data transmission: 
	- in one direction only (simplex), from sender to receiver.  
	- The communication channel is assumed to be error free,
	- and the receiver is assumed to be able to process all 
	the input infinitely fast.
	
	Consequently, the sender just sits in a loop pumping 
	data out onto the line as fast as it can. 
	*/
	
	typedef enum {frame_arrival} event_type;
	
	#include "protocol.h"
	
	void sender1(void)	// will run on sender side
	{
		packet buffer; /* buffer for an outbound packet */
		frame s;       /* buffer for an outbound frame  */
		
		while (true)   /* forever */
		{
			from_network_layer(&buffer); /* go get something to send */
			s.info = buffer;             /* copy it into s for transmission */
			to_physical_layer(&s);       /* send it on its way */
		}
	}
	
	void receiver1(void)	// will run on receiver side
	{
		frame r;          /* buffer for an incoming frame */
		event_type event; /* filled in by wait_for_event(), but not used here */
		
		while (true)
		{
			wait_for_event(&event);    /* only possibility is frame_arrival */
			from_physical_layer(&r);   /* go get the inbound frame */
			to_network_layer(&r.info); /* pass the data to the network layer */
		}
	}
	```

- Key Assumptions : 
	- Drop the most unrealistic restriction used in protocol 1:
		- The ability of the receiving network layer to process incoming data infinitely quickly (i.e. no flow control is required) *or*	
		- The presence in the receiving data link layer of an infinite amount of buffer space in which to store all incoming frames while they are waiting their respective turns
	

- **Simplex Stop-and-Wait Protocol 2**

	- When does the feedback generated ?
		> When receiver sends the `s.info` to network layer, then the frame of that packet will be empty and there will be free storage in buffer to now receiver can send the empty packet as feedback to sender.
		
		> As protocol is simplex, there will be not other data except control bytes. so we can easily send this empty packet.

	```c
		/* Protocol 2 (stop-and-wait) also provides for 
		- a one-directional flow of data from sender to receiver. 
		- The communication channel is once again assumed to be error free, 
		as in protocol 1. 
		- However, this time, the receiver has only a finite buffer
		capacity and a finite procesing speed, so the protocol must 
		explicitly prevent the sender from flooding the receiver 
		with data faster than it can be handled. 
		
		The solution is to use acknowledgement frames.
	
	*/
	
	typedef enum {frame_arrival} event_type;
	
	#include "protocol.h"
	
	void
	sender2(void)
	{
		packet buffer;     /* buffer for an outbound packet */
		frame s;           /* buffer for an outbound frame */
		event_type event;  /* frame_arrival (ACK) is the only possibility */
	
		while (true)
		{
		from_network_layer(&buffer); /* go get something to send */
		s.info = buffer;             /* copy it into s for transmission */
		to_physical_layer(&s);       /* send off the frame */
		wait_for_event(&event);      /* do not proceed until an ACK received */
		// here we are only waiting for ACK frame (Feedback frame)
		}
	}
	
	void
	receiver2(void)
	{
		frame r, s;        /* buffers for frames */
		event_type event;  /* frame_arrival is the only possibility */
		while (true)
		{
		wait_for_event(&event);    /* only possibility is frame_arrival */
		from_physical_layer(&r);   /* go get the inbound frame */
		to_network_layer(&r.info); /* pass the data to the network layer */
		to_physical_layer(&s);     /* send a dummy frame (ACK) to awaken sender */	// As we can see that `s` variable is completely empty (i.e. dummy frame)
		}
	}
	```
	
- ## Positive Acknowledgement with Retransmission
	- Normal situation of a communication channel that makes errors
	- Frames may be either damaged or lost completely
	- Assume that if a frame is damaged in transit, the receiver
	hardware will detect this when it computes the **checksum**
	- <u>It seem that a variation of protocol 2 would work: adding a timer where timeout will retransmit a frame</u>
	
- ## Positive Acknowledgement with Retransmission
	Consider
	a)The network layer on A gives packet 1 to its data link layer. The packet is correctly received at B and passed to the network layer on B. B sends an acknowledgement frame back to A.
	b)The acknowledgement frame gets lost completely.
	c)The data link layer on A eventually times out and sends the
	frame containing packet 1 again
	d)The duplicate frame also arrives at the data link layer on B perfectly and sent to network layer.
	The protocol will fail. Some way for the receiver to be able to
	distinguish a frame that it is seeing for the first time from a
	retransmission is needed
	
	- <u>It will not work by just simply adding timer to protocol. 2</u>
	- Addition of sequence number can solve the problem.
	
	
	
	- Since a small frame header is desirable, the question arises: **What is the minimum number of bits needed for the sequence number?**
		- The number of bits require to store the sequence numbers will depend on the environment.
		- <u>MINIMUM `1 bit` is sufficient for this!</u>
	
	- The only ambiguity in this protocol is between a frame, m, and its direct successor, m + 1.
	- If frame m is lost or damaged, the receiver will not acknowledge it, so the sender will keep trying to send it.
	- Once it has been correctly received, the receiver will send an acknowledgement to the sender.
	- Depending upon whether the acknowledgement frame gets back to the sender correctly or not, the sender may try to send m or m + 1.
	- A 1-bit sequence number (0 or 1) is therefore sufficient
	
- ## **Simplex stop and wait protocol for a noisy channel (1)**
	- <u>Positive Acknowledgement with Retransmission (PAR)</u>
	```c
	/*
	Protocol 3
	Assumes:
	The channel is noisy and we can lose frames (they never arrive).
	Simple approach, add a time-out to the sender so if no ACK after a certain period, it retransmits
	the frame.
	Scenario of a bug that could happen if we’re not careful:
	A transmits frame one
	B receives A1
	B generates ACK
	ACK is lost
	A times out, retransmits
	B gets duplicate copy of A1 (and sends it on to network layer.)
	Use a sequence number. How many bits? 1-bit is sufficient for this simple case because only
	concerned about two successive frames.
	Positive Acknowledgment w/ Retransmission (PAR): Sender waits for positive acknowledgment before
	going to next data item.
	*/
	/* Protocol 3 (PAR) allows unidirectional data flow over an unreliable channel. */
    #define MAX SEQ 1 /* must be 1 for protocol 3 */	//MAX was defined in protocol 1
    typedef enum {frame_arrival, cksum_err, timeout} event_type;
    #include "protocol.h"
    void sender3(void)
    {
        seq_nr next_frame_to_send; /* seq number of next outgoing frame */
        frame s; /* scratch variable */
        packet buffer; /* buffer for an outbound packet */
        event_type event;
        next_frame_to_send = 0; /* initialize outbound sequence numbers */
        from_network_layer(&buffer); /* fetch first packet */
        while (true) {
            s.info = buffer; /* construct a frame for transmission */
            s.seq = next_frame_to_send; /* insert sequence number in frame */
            to_physical_layer(&s); /* send it on its way */
            start_timer(s.seq); /* if answer takes too long, time out */
            wait_for_event(&event); /* frame_arrival, cksum_err, timeout */
            if (event == frame_arrival) {	// If any thing goes wrong then the frame will be discarded and while  loop continues to send that frame again
                from_physical_layer(&s); /* get the acknowledgement */
                if (s.ack == next_frame_to_send) {
                stop_timer(s.ack); /* turn the timer off */
                from_network_layer(&buffer); /* get the next one to send */
                inc(next_frame_to_send); /* invert next frame to send */
                }
            }
        }
    }
    void receiver3(void)
    {
        seq_nr frame_expected;
        frame_r, s;
        event_type event;
        frame_expected = 0;
        while (true) {
            wait_for_event(&event); /* possibilities: frame_arrival, cksum_err */
            if (event == frame_arrival) { /* a valid frame has arrived */		// If any problems occurs then this block will not execute so that sender will retransmit the frame. (will WAIT until sender sends it again)
                from_physical_layer(&r); /* go get the newly arrived frame */
                if (r.seq == frame_expected) { /* this is what we have been waiting for */
                    to_network_layer(&r.info); /* pass the data to the network layer */
                    inc(frame_expected); /* next time expect the other sequence nr */
                }
                s.ack = 1 − frame_expected; /* tell which frame is being acked */
                to_physical_layer(&s); /* send acknowledgement */
            }
        }
    }	
	```

- Protocol number 1 to 3 are SIMPLEX protocols and next protocol number 4 to 6 are DUPLEX protocols.
	- So up to now, we were writing two different functions for sender and receiver but from now onwards, we will write only one function which works for both sender and receiver