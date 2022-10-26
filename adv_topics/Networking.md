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

* Topic 1
	* Details
	* Details
	* Details
* Topic 2
	* Details
	* Details
	* Details
