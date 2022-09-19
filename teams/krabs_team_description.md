# K*rust*y Krabs

## Canonical game repo URL:

https://github.com/cs1666-krabs/game

## Team Members

* Advanced Topic Subteam 1: Procedural Generation

	* Matthew Glazar
		* Pitt Username: mag387
		* Github Username: MatthewGlazar

	* Aidan Walsh
		* Pitt Username: ajw137
		* Github Username: Codenameaidan

	* Wilson Biggs
		* Pitt Username: wab41
		* Github Username: w-biggs

	* Ryan Chakov
		* Pitt Username: rac223
		* Github Username: RyanChakov

* Advanced Topic Subteam 2: Networking

	* Tobias Hildebrandt
		* Pitt Username: toh34
		* Github Username: tobias-hildebrandt

	* Nicholas Thompson
		* Pitt Username: nat82
		* Github Username: xney

	* Daniel Hopping
		* Pitt Username: dsh57
		* Github Username: hoppingd

	* Alex Haskovec
		* Pitt Username: ajh191
		* Github Username: AlexHaskovec

## Game Description

Our game is a multiplayer downward scrolling adventure game where the players’ goals are to collect resources and discover what is deeper down in the world through mining blocks and exploring caves.

## Advanced Topic Description

### Procedural Generation

We will procedurally generate terrain on a vertically-infinite 2D grid, including ore clusters, biomes, and structures. Generation will use a noise function and a random number generator.

### Networking

We will support real-time multiplayer using a server-client architecture. Players will be able to coexist in the same game world and interact with it at the same time. The server and clients will communicate via a custom protocol built on top of UDP. This protocol will enable synchronization of relevant information including player state and world state. As a stretch goal, we will create a server browser that will allow players to easily join servers.

## Midterm Goals

* General
	* Save and load game state
	* Player movement
* Procedural Generation
	* Simple generated terrain in a finite world
	* Cave generation
* Networking
	* Server that can support at least one client
	* Synchronization between server and client(s)

## Final Goals

* General (20%)
	* 5%: User interface
	* 5%: Simple inventory
	* 5%: Mining
	* 5%: 60 FPS
* Procedural (30%)
	* 10%: At least 2 distinct biomes
	* 10%: Infinite world (downward)
	* 10%: Ore generation
* Networking (30%)
	* 10%: Only sync changes, not entire state
	* 15%: Can sync at least 4 clients
	* 5%: Single-change sync occurs in less than 1 frame

## Stretch Goals

* Unique underground structures
* Server browser
