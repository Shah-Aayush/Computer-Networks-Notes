# Lecture 12

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
	
	void sender1(void)
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
	
	void receiver1(void)
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
		- The ability of the receiving network layer to process incoming data infinitely quickly *or*
		- The presence in the receiving data link layer of an infinite amount of buffer space in which to store all incoming frames while they are waiting their respective turns

- **Simplex Stop-and-Wait Protocol 2**

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
		to_physical_layer(&s);     /* send a dummy frame (ACK) to awaken sender */
		}
	}
	```
	
	