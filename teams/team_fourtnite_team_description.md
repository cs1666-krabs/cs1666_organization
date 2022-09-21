# Team Fourtnite

## Canonical game repo URL:

https://github.com/chris-hinson/waste

## Team Members
* Advanced Topic Subteam 1: Procedural Generation

	* Christopher Hinson
		* Pitt Username: chh183
		* Github Username: chris-hinson
	* Gavin Heinrichs-Majetich
		* Pitt Username: gmh33
		* Github Username: Elsklivet
	* Camryn Simons
		* Pitt Username: crs163
		* Github Username: camrynsimons
	* Dan Li
		* Pitt Username: til61
		* Github Username: til61

* Advanced Topic Subteam 2: Networking

	* Caela Go
		* Pitt Username: cmg139
		* Github Username: cmgo412
	* Chase Bradley
		* Pitt Username: clb234
		* Github Username: clb234
	* Nathan Myers
		* Pitt Username: nmm103
		* Github Username: nmm103
	* Prateek Jukalkar
		* Pitt Username: psj4
		* Github Username: psdev30

## Game Description

We plan on telling a loose storyline following the player, one of the few survivors of a terrible apocalypse, and their journey to undo the horrors that have ravaged their homeland.  The player will be motivated by the promise of a powerful cleansing artifact left behind at the epicenter of the world’s destruction, but will be progression-gated by a series of powerful enemies they must defeat to venture deeper into the danger zone.  Apart from these sparse goals, the player is free to roam the world as they wish, collecting and training a team of loyal monsters to aid them in their goal, or simply just finding what is left of the place they once called home.

We have set out to make a creature-collecting rpg set in a post-apocalyptic world. Featuring a turn-based combat system, loyal monsters to collect and battle, and a vast world full of power items to discover, this game falls firmly in the vein of classic titles such as Pokemon, The Legend of Zelda, Final Fantasy, and Dragon-Quest.  Our core gameplay loop is borrowed from pokemon, and revolves around the concept of defeating increasingly strong enemies, relying upon capturing and training our own fighters to do so. This explore-capture-train progression loop creates a positive feedback cycle, where the player is rewarded for time invested in the game, in turn encouraging them to invest more time. 

Our game is set apart from others by three core concepts: Monsters/Battling, Procedural Generation, and Multiplayer.

### Battles 

Battles take place on their own screen that is cut to when entering the battle. The Battle Screen presents your Monster Trainer’s Monster facing another Monster in a battle with UI that tracks basic creature info for each of them (health, level, your creature’s total actions). Differently from Pokemon, the game operates with a turn-based system that gives the first turn of action to whichever Monster has the highest speed stat initially. During a turn, a creature can perform a number of Attacks/Moves equal to the total actions that can be performed by them. 

Our basic battle mechanics should be a 'Type' damage-system, actions that do damage or defend against damage, and multi-action combat that lets you do multiple moves in a turn. Battle mechanics here are focusing on stats but without changing them or the battle pattern, and include 'Attack' and 'Defend' moves. Advanced battle mechanics would then focus on Moves that change how a battle is played. This would include Moves that change the turn order or actions taken per turn combat, change the stats of the enemy/your Monster, or even force you or your enemies' Monster out to different Monster that is in your fighting Party. These moves are under the category 'Special' as each move should act on stats, not damage values (though indirectly may affect damage calculations)


#### Types & Moves

To fit our future wasteland theme, we are implementing our own typing system that mimics the elemental strengths/weaknesses systems present in many JRPGs. When an Attacker damages a Defender, any strengths or weaknesses are included in damage calculations. Our goal with types is to invite design reminiscent of post-apocalyptic themes, while staying grounded so that the design plays well and can be picked up on quickly. Our current goal is 6-8 types for the final game, but if possible we could come up with 9-12. Design challenges regarding developing the base movesets for each type could include having each type be strong in some very specific way (e.g. Robot Type has high ACT, Rad Type has an abnormally strong Attack move early.) Each type should have 1-2 Attack, Defense, and Special moves each and have 4 known moves maximum, so we expect to develop around 24-30 technically distinct basic moves and 10-12 more unique special moves.


## Advanced Topic Description

### Networking

We will support multiplayer gameplay with two players competing against each other through a peer-to-peer networking model. For the transport protocol, we will likely use TCP due to its reliability and guarantee that packets will arrive at the server in the order they were sent. TCP maintains strict ordering; if a packet is lost in the transmission process, none of the packets that did arrive can be processed. Since we are implementing a turn-based game, we do not believe the added latency from TCP’s behavior will be an issue and will also disable Nagle’s Algorithm, which buffers together packets before sending them and increases latency. However, if it becomes necessary, we would consider pivoting to a custom UDP-based protocol. In terms of transmitting data between clients, we plan to implement our own message passing communication protocol. The primary goal, however, is to ensure that players take their turns in the correct order. Initially, we will make the game playable over LAN and once this functionality is in place, shift to adding fully online gameplay. 

    
### Procedural Generation

The overworld play area will be mostly procedurally generated using an algorithm such as Wave Function Collapse. Story-critical locations could be anchored to the map and have areas surrounding them procedurally generated. In this way, the game would be semi-open-world. When a “new game” is started, the world is procedurally generated a single time (in a sort of roguelike fashion). Using the Wave Function Collapse algorithm, 16*16 logical px tiles will be the initial inputs that resemble different themes of our map. Tiles would be assigned adjacency rules such that, when generating new tiles, tiles can only be placed in a way that satisfies the adjacency rules of the tiles they would be placed next to. This allows for random generation of play area without weird glitching where impossible land layouts are drawn. As each tile is drawn, a propagation algorithm runs to draw its neighbors, until all tiles are generated. Additionally, we would supply a frequency matrix that tells the procedural generation algorithm to prefer placing certain tiles more often than other tiles. We considered making it so tile-specific mods, such as monsterCanSpawn, treasureCanSpawn, playerIsSlow, or strongerRad as a few examples, would be considered in creating frequency matrices so that when generating tiles there will be an approximate ratio of “normal” tiles of a certain kind to tiles that have specific modifiers. For example, the frequency of SwampWater may be 0.75 and the frequency of SwampWaterMonsterCanSpawn may be 0.25. This may be unnecessary, though, and could instead be replaced with a struct-level randomly generated boolean with hard-coded probability so that there is only one overarching struct SwampWater with a single generation frequency. Additionally, we considered using procedural generation with the Markov Junior algorithm to generate monster assets, but decided to opt instead for selecting parts from a pool of possibilities (“Mr. Potato Head” style generation).

## Midterm Goals

* World Viewable	Creating a viewable world
* World Gen			Randomly Generating World
* Walkable			Let Player move around that world
* Population		Spawn Monsters in World

## Final Goals

* Battling	Interact with Monsters
* Networking	Battle others

## Full Rubric
| Monsters:20%   |                          |                                                                                                                                                |
| -------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 5              | Spawning System          | Monsters can spawn in appropriate areas in the overworld                                                                                       |
| 5              | Typing System            | Monsters have a distinct type which has its own strengths and weaknesses                                                                       |
| 5              | Moveset System           | Monsters have a distinct moveset, unique and appropriate to its typing system                                                                  |
| 5              | Leveling System          | Monsters can be trained and leveled                                                                                                            |
| Battles:20%    |                          |                                                                                                                                                |
| 10             | PvP battles              | Players can battle other players                                                                                                               |
| 10             | PvE battles              | Players can battle boses alongside other players                                                                                               |
| Proc Gen:20%   |                          |                                                                                                                                                |
| 10             | WFC World                | Propagation algorithm runs so that WFC recursively generates chunks                                               |
| 5              | WFC Adjacency Rules      | Tiles can correctly be generated around collapse anchors according to given adjacency rules; including that WFC cannot overwrite anchor points |
| 5              | WFC Frequency hints      | WFC can allow for controlling frequency of tiles being placed using a frequency hints matrix                                                   |
| Networking:20% |                          |                                                                                                                                                |
| 10             | Connect two instances    | Two players' games can find and connect to each other                                                                                          |
| 5              | Battling Protocol        | Two players can communicate battle data to each other                                                                                          |
| 5              | Trading Protocol         | Two players can give monsters and items to each other                                                                                          |
|                |                          |                                                                                                                                                |
|                |                          |                                                                                                                                                |
| Stretch goal 1 | Fixed points/Side Quests | Add a number of fixed locations and story quests into the game's world generation                                                              |
| Stretch goal 2 | Advanced battling        | Add more advanced and unique battle mechanics such as multi-moves and item usage                                                               |

## Stretch Goals

* Quests			Side Quests and storyline
* Advanced battles	Add more advanced and unique battle mechanics such as multi-moves and item usage
