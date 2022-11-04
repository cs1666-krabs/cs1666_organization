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

* Intro to Talk/Review of Physics Systems
	* Why are physics systems important as a game mechanic?
		* Physics system are game system that are already familiar to players since they replicate the interactions of objects in the real world
	* BOTW
		* Physics-based puzzles
	* Superliminal
		* Object (and collision) resizing based on perspective
	* Noita
		* Every pixel simulated
		* Solids, liquid, gas
		* Sand simulation
* Rigid Body
	* Applying forces, velocity to objects that maintain a consistent boundary
		* Can only directly manipulate object’s transform (i.e. position)
		* Kinematics equations
	* How to produce smooth acceleration/deceleration?
		* Keep track of object’s current velocity in both x and y-axises
		* Increment transform by the velocity
		* Apply forces through adding a constant value to the object's velocity as long as the force is being applied to the object
		* Scale by timestep for consistent object transform updates regardless of framerate
	* Collision resolution
		* Application of forces to objects as a result of collisions
		* Inelastic collisions are when one or both objects absorb the impact of the collision (in real world this occurs through external forces such as friction or heat)
		* Elastic collision results in the total momentum of the system being conserved (both objects bounce off each other from a collision)
		* Masses work as scalars to collisions (heavier objects carry more momentum compared to lighter objects)
			* Not concerned about this in our code at the moment

* Collision Detection Algorithms
	* SAT (Separating Axis Theorem)
		* We know how AABB works
			* What do polygons that are not circles or rectangles do in AABB?
			* How does a rotated polygon interact with AABB?
		* How are polygons defined within an engine
			* We do not care about the edges of a polygon
			* Shapes are defined by vertices
			* We store them in an array that shows adjacency
			* We draw around these vertices
		* Introduce separating axis
		* Create our axes
			* Show a polygon with all lines extended outwards
			* Make a line normal to all lines extending outwards
			* Show code for this process
		* Create a shadow of the polygon onto an axis
			* Project every vertice onto this line
			* Now that every vertice is projected how do we know which vertices are actually describing the shadow of the shape
			* Look for the largest vector and the smallest vector
				* These describe the shadow of the shape
			* Show several shapes shadows, including circles and triangles
				* Show how a line might have trouble with this
		* Now we do this for both shapes
		* Compare the axes shadows to see if they are in each other
		* Get information about this collision to find how to remove a polygon outside of another
		* Why this is a good system
			* Very fast
			* Do not need to know the rotation, simply the vertices
			* Easy to implement
		* Disadvantages
			* Cannot do concave polygons
			* Cannot do lines
			* Does not tell you what areas collided
		* Workarounds
			* Concave polygons
				* Make the the shape into several convex polygons
			* Lines
				* Make a line an incredibly thin triangle
			* Collision
				* Do some hacky math

		
