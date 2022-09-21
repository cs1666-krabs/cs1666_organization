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

Our game is a multiplayer adventure/sandbox game. Players will be able to explore and dig in an infinite, procedurally-generated, vertically-scrolling 2D grid world. Players will be able to join together in a multiplayer world to mine blocks, collect resources, and delve deep underground to discover what lies below.

## Advanced Topic Description

### Procedural Generation

We will procedurally generate terrain on a vertically-infinite 2D grid, including ore clusters, biomes, and structures.  The surface will be created to look vaguely like a beach biome, and will be generated using a 2D Perlin Slice.  Below the surface, we will use noise functions (probably Simplex Noise or Perlin Noise, possibly in combination with Perlin Worms for longer caves) and a random number generator.  It should be expected that we will experiment with different noise functions and view their outputs until we uncover what works the best.  Mineable ores will be generated in conjunction with these open caves, and will be placed at random intervals.

### Networking

We will support real-time multiplayer using a server-client architecture. Players will be able to coexist in the same game world and interact with it at the same time. The server and clients will communicate via a custom protocol built on top of UDP. This protocol will enable synchronization of relevant information including player state and world state. As a stretch goal, we will create a server browser that will allow players to easily join servers.

## Midterm Goals

* Save and load game state
* Player movement
* Display basic finite, static map
* Server that can support at least one client
* Communication between server and client(s)

## Final Goals

* General (20%)
	* 10%: Players can mine blocks into inventory
	* 10%: UI that displays inventory
		* Display only, no interaction
* Procedural Generation (30%)
	* 10%: Infinite world (downward)
	* 10%: Cave generation
		* Players should almost always be able to see a cave on screen
		* Perlin/Simplex noise, maybe Perlin worms
	* 5%: At least 2 distinct biomes
		* Changes ore generation and structure frequency
	* 5%: Ore generation
		* Clumps of rare, unique blocks
* Networking (30%)
	* 10%: Synchronizes game state
	* 15%: Can sync at least 2 clients
	* 5%: Efficient state synchronization

## Stretch Goals

* At least 1 type of generated underground structure
	* Buildings, mineshafts, trees, etc
* Support at least 4 players in multiplayer
