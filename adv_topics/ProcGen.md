# Procedural Generation advanced topic presentation outline

## Presentation 1

* Topic 1: The history of Proc Gen
	* What is procedural generation?
		* Definition and origin
	* What are some of the broad uses and possibilities?
		* Simulation
		* modeling
		* graphics

* Topic 2: The History of Proc Gen in Video Games
	* How does proc gen apply to video games specifically
		* What does it add to the game
			* User experience
			* Replayability
	* Different approaches & algorithms
		* Examples:
			* Binding of Isaac (2d room)
			* Terraria (2d rand block)
			* No Man’s Sky (the better/updated version) (3d terrain)

* Topic 3: Our planned implementation
	* Describe A*
	* Describe Steps
		* Randomly generating room sizes & locations
		* Delaunay triangulation to find room paths and create graph
		* Create Minimum Spanning Trees & insert edges
		* A* to find paths


## Presentation 2

* Topic 1: Original WFC
	* General definition
		* WFC algorithm: generates bitmaps that are locally similar to the input bitmap
	* Implementation in different languages and games
		* Languages: C++, Python, Rust, Kotlin, Go, JavaScript 
		* Games: Bad North, Caves of Qud, Townscaper
	* Simplification of algorithm
		* Use everyday example to demonstrate the basics of the WFC algorithm
		* Key components for simplification:
			* Considering all possible options for a certain point, and then collapsing that point
			* Continuing process until all elements are collapsed
			* If all elements are collapsed, then the output is good and can be returned
			* A contradiction may occur, which means the algorithm was unsuccessful. Have to start again or revert to a certain point
	* Detailed step-by-step of algorithm
		* Inputs for the algorithm
			* NxN patterns
		* Initializations(set-up) 
			* Array of elements
			* Coefficients 
		* Main part of the algorithm(iterating until a certain condition is met)
		* Completely observed state vs. contradiction 
			* Return output vs. nothing returned
				* Discuss options for contradiction(nothing returned)
	* Transition into tiling WFC
		* Lots of room for simplification with current state of algorithm 
* Tiling WFC and Rule Generation 
	* A simplification of the bitmap generation, where the “wave” is every permutation, the approach we take takes advantage of tiling.
		* Tiles reduce the information we need to keep track of, while preserving essential information
		* Tiles allow us to make the world map more interactive
	* How to make adjacency rules
		* Hard code into game
			* Used on PoC and simple tile relationships to test collapse functions
			* Not really doable with complex maps we want to mimic
			* n^2 rules for n tile types  
		* Read and generate adjacency rule sets with input representation of a map
			* Can generate rule sets that capture every possibilities in the input
	* Iterates over input in row-major order
		* Reads each tile and looks at its neighbors
		* Creates entry in hashmap for this tile with each direction and the neighbor found there
			* HashMap only keep a single occurrence of each tile type
				* Unrealistic result
			* Vectors sounds nice
				* Too much extra space
			* Trade-off: we are storing frequencies of the input map
		* Repeat and update until all rulegen is finished
	* Downsides
		* The rule set may be too strict, which will lead to long runtime
			* Consider an extreme situation where there’s only one solution
		* The rule set may not be as comprehensive as it can be
			* That’s okay, we can easily change the representation of the input map to add/remove relationships.

* Recursive algorithm in detail
	* Start by choosing a tile to collapse
		* This is based on minimum entropy
			* Entropy is how many possible subpositions we can choose for this tile
			* Less possible subpositions means we should collapse sooner
		* Example code for choosing tile
	* Then we start to collapse tiles starting at the one we chose initially
		* First check if our board is solved
			* This checks if our board is in a valid position:
				* No tiles are in places that their or their neighbor’s adjacency rules disallow
			* Then it checks that all tiles are collapsed
		* Creates a backup of the superposition of the current tile
			* We will use this to return to this state if we fail to get to a valid state
		* We then shuffle the currently possible subpositions for this tile
		* Iterate over all of the subpositions (which are now in random order)
			* Set the collapsing tile’s type to the subposition
			* Update all of the neighboring tiles’ superpositions so that they reflect the change
				* Code example with retain
			* Check if we have put ourselves in a valid position
				* If so, continue to collapse
				* If not, set our neighbors’ superpositions back to normal and try the next subposition
		* If, after trying all positions for this tile, none result in a valid position, then reset the current tile completely to its backup state and return a failure
	* Looking forward at things we need to implement
		* (These may be finished by the time the presentation rolls by!)
		* Frequency control
			* Modify the algorithm to track the frequency with which tiles show up in our input boards
			* Change our random subposition selection to be based on frequency
				* This could give us much more realistic looking worldgen, and much more granular control
		* Seeded rows and columns
			* To generate an infinite world, we will not generate everything at once, meaning we will need to generate chunks neighboring existing chunks
			* To ensure the chunks align across screens, need to seed neighboring rows and columns to restrict them
		* Allow for generation in background threads
			* Infinite worldgen should happen all the time
		* Create fixed locations on the map with PRNG layers overtop of WFC
	* Uses recursion to aid backtracking
		* Undo bad decisions and make new attempts until we end up in a valid state
		* This is very time and memory consuming!
			* Can take several seconds just to generate a few screens
			* Not nearly as simple as something like Perlin noise
				* And backtracking is always a killer
					* Think back to 1501 crossword project
			* Run into stack overflows if too many stackframes are made
				* Currently the code spawns the generator in its own thread with 4MB of stack space to avoid overflowing
	* This leads to a problem, we’re not running fast enough nor using little enough memory to keep the experience flowing
		* Need to optimize… (flows into next section)

* Optimizations
	* 2 main fields of optimization
	* Performance opt
		* Make it iterative (work in progress)
			* Considered using a stack and popping off bad decisions to undo them
			* Didn’t work, might’ve been a bug in our implementation but was largely unsuccessful in creating a valid board
			* Using an iterative approach would reduce the load on the callstack and thereby memory
		* Better rulegen
			* Convert tile types to enum variants instead of usizes
				* Better for code readability and re-use
			* Requires the use of proc macros
				* Enum variants must be constructed at compile time, rather than runtime
				* This also means that all rulegen must be done in a separate phase before the map generation
					* This only needs to be run once for given inputs though, and may subsequently be used to generate as many tilemaps as desired
				* Proc macros as essentially compiler plugins for rustc and while extremely powerful, are also extremely complex
	* More natural looking output
		* NxN tilegen
			* Original algorithm specifies input of NxN tiles, rather than a single pixel
				* While we are outputting NxN tiles, we are representing them in input as a single pixel (technically a number)
				* This can lead to a loss of detail and less natural looking output
		* Symmetry rules
			* Original algorithm also gives rulegen time information about the symmetry of tiles
				* This allows placing tiles on different sides than they are seen in the input image, leading to more generalized, natural looking output, along with faster generation
		* Frequency counting
			* Original algorithm also specifies that input tile pattern frequency should be taken into account when generating, so proving this information at rulegen time should also lead to more natural looking output
 

## Presentation 3

* Topic 1: Natural 2D Terrain with Procedural Generation
	* Intro & Infinite World
		* Intro:
			* So we want to create a sort of natural 2D world…
				* Similar in style to Terraria.
			* We want something that looks smooth-ish, like nature.
			* There is no end goal or end really it is going to be infinite
			* Can't manually create an infinite world 
		* Infinity
			* Fractioned generation
				* Can't generate everything all at once 
			* An infinitely long world would cause infinitely large amount of ram
				* We have to spawn and despawn chunks as we approach them
			* Deterministic Seed 
				* Why you need it to be deterministic
			* Chunk borders would cut off different generations like caves and ore veins so keep that in mind in infinite generation
	* World surface (Aidan)
		* Pure noise sucks. Impossible to navigate, uninteresting to explore.
		* Except, when we zoom in, doesn't look too bad… we got some "mountains" and "valleys" here. 
			* So we can create a line between the points and generate block height from that…
			* Yeah, but a line isn't great though. Still really jagged.
			* Let's smooth this out (Interpolate between points).
				* Interpolation algorithm:
					* where it comes from
					* The formula itself
					* What it looks like, graphed
			* Okay, so how do we implement that in a game?
		* Discussion of actual 1D perlin algorithm using setup above
			* Basically generate points and interpolate between them.
			* (Show code)
			* Scaling height and width of hills/valleys
		* Let's use multiple slices.
			* Depth of sand/dirt
		* Let's use another slice to shift everything left / right
			* More interesting; creates overhangs.
		* Alternate perlin noise algorithms
			* Sin function: sin (2 * x) + sin(pi * x)
				* Isn't periodic → therefore, can use values along this function.
	* Caves (2D perlin noise) (Matt)
		* Hashing
			* X,y
			* Needs to be different in each game
			* How hash table is implemented
		* Gradient
			* What gradient is
			* How it is calculated
		* Linear interpolation
			* Concept
			* Implementation
		* Fade Function
			* Purpose
			* Algorithm
		* Thresholding
			* Purpose
			* Visualization
			* Parameters
	* Biomes + Ore Generation (Wilson)
		* Ore generation
			* The way ore veins look is a bit different from the "clouds" that Perlin noise is best for
			* Random polygons? Random lines?
				* Random lines are simpler
			* How ore generation is implemented step-by-step
				* For each chunk, randomly determine how many veins to generate
					* Seed
				* Generate a seed for this vein based on the current vein
					* Generate start coordinate
					* Generate end coordinate - Y must be below current coord
					* Generate thickness
				* To find out if a block is inside the vein, find distance to line and check if within thickness
					* Formula for distance from point to line segment is somewhat complex
				* How we store ore veins (todo: actually reimplement that how Tobias was saying)
		* Biomes
			* Different approaches are possible - Perlin noise clouds, Perlin slices
				* Slices are already used for transition from sand to stone, which is very similar to what we want for biomes
			* How biomes are implemented step-by-step
				* How the code decides when to switch from one biome to the next
			* We now have these biomes…
				* …which contain these ores
	* Structures (Ryan)
		* How structures are implemented 
			* Follow a rule set in empty space 
			* Have a tree expand in the space provided 
		* Perlin worms
			* Algorithm
			* Mineshaft depiction 
	* Conclusions
		* Thanks!
