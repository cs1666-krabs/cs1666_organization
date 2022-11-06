# Networking advanced topic presentation outline

## Presentation 1

* Focus of Presentation
	* client-server based, not peer-to-peer
	* real-time action, needs to be quick and responsive, e.g. FPS, RTS, etc
	* our goal: allow players to have fun playing a game together
* TCP is cool, but problematic; why we must use UDP
	* we like: reliability/ACKs; congestion/flow control; connection handshake; sequence numbers; possibility of TLS
	* we don’t like: latency; forced in-order delivery; forced retransmissions
* We must accept that packets can be lost
	* assume anything can be lost, so make sure to send a state
	* if you need to guarantee something arrives, write a simple ACK/retransmission system
* Messages
	* clients send input and state
		* but don’t trust the client to tell you its true state (cheaters exist)
	* server sends updated state and also other inputs
		* server is the authoritative source of information
		* other inputs allow for clients to do simple predictions about the future on packet loss
* Lag compensation (there is always lag!)
	* buffer packets from all clients (creates consistent lag)
	* lie to the players in order to make them feel better; show an event before it’s confirmed by the server
		* simulate physics locally (client-side prediction, non-authoritative)
		* players hate input lag!
	* change your gameplay if it’s unfun because lag (and lag in unavoidable!)
* Synchronization (replicating state)
	* don’t need to send entire state to each client
	* they only need to know what’s relevant to them
	* if state is large, prioritize what’s important
		* eventually the most current state will arrive
	* delta compression: send difference in state, relative to a state that we know the client knows
	* quantization: floating point operation results can vary depending on architecture, compiler, etc


## Presentation 2

* Overview of our topics
	* What are the differences between TCP and UDP (on a macro level, key features)
	* When would you use a TCP connection vs when would you use a UDP connection
	* Server-client connection vs a P2P connection
		* Use cases and why?
* Explanation of an example connection
	* Initially, we planned on making our game TCP-based. Why?
		* TCP demo code explanation
	* We switched to UDP. Why?
		* UDP demo code explanation
* What does code look like in our particular game?
	* Should we use a client-server connection or should we make a P2P connection?
	* Why did we make the decision to make our game P2P?
		* What are future considerations/drawbacks of making that decision?
	* Setting up a player's UDP Socket
	* Channels vs Mutexes to communicate with host() or client()
		* Problems with channels and mutexes
* What we want to do and how we're gonna do it
	* Networking with more than two people (Multiple player battles)
		* Good thing we switched to UDP
	* Trading items between players:
		* What unique challenges this has/will impose
	* What should we have done differently in retrospect?
		* Planning for the future
			* Forethought would have made our lives easier  
