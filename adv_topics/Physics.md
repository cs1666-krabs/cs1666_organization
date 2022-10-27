# Physics advanced topic presentation outline

## Presentation 1

* History of Physics (10 minutes)
	* Video game physics have existed about as long as games themselves
	* Early games used pre-rendered animation over real-time math calculations
		* Why this was popular / why it no longer is
	* Goal of a physics engine is to visually represent physics to the user; not accurately portray physics
		* Allows game developers to take shortcuts
	* The complexity of calculations and number of factors combined with technical restraints can often lead to bugs
	* Physics goes into things we won’t be discussing too, like shading, ragdoll physics, etc.
* Rigid Body Dynamics (10 minutes)
	* Acceleration
	* Gravity
	* Simulating the effects of collision detection
* Breakable Objects (barrels, walls, etc) (10 minutes)
	* What are particle systems?
	* The typical implementation of a particle system
		* Emitting new particles
		* Simulation and updating parameters
		* Rendering particles
	* Melee vs. range attacks
	* Different sprites denoting level of damage
* Barrels (10 minutes)
	* Common use of barrels in video games
		* Cliche of exploding barrels in video games
		* Why they are a nice feature to add
	* HP design similar to enemies
	* Once HP hits 0, barrel will explode and release ten projectiles traveling in random directions at random velocities.
		* generate random x velocity
		* generate random y velocity
		* x= x0 + v0xt+ 1/2axt^2
		* y = y0 + v0yt+ 1/2gt^2
	* These projectiles can damage players, objects, and enemies based on their velocity.
* Projectiles (5 minutes)
	* Arced Projectiles (bow and arrow, barrel stuff) affected by gravity as well as collisions, similar to player motion but with constant horizontal velocity
	* When colliding with another object, the collided object/enemy’s HP will be reduced

			
		

## Presentation 2

* Topic 1
	* Details
	* Details
	* Details
* Topic 2
	* Details
	* Details
	* Details
