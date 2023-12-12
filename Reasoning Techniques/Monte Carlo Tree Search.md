![[Screenshot 2023-11-07 at 11.49.43 AM.png|500]]

* Build gradually a search tree and start sampling
	* Basically simulating the game by random samples and keep track how well you perform from given starting position
* [[Best-first search]]
* Very popular, very successful 

![[Screenshot 2023-11-07 at 11.51.01 AM.png|500]]
We aim for 100%, so for sure a win.

Exploitation says lets focus on the promising nodes.
Exploration says uu let's explore a bit maybe you're wrong.

TODO add 6 sec animation from this slide

**Selection**
* Traversal from the root until we reach a position which is not part of the tree
* *Selection Policy*: Controls exploitation and exploration balance
* Multi-Armed Bandit Problem
	* find a slot machine that won't fuck you over
* Upper Confidence bounds for Trees: UCT
	* this is the bound for finding the machine
* Selects the child k of the node p according: $$k \in argmax_{i \in I}(v_i + C \sqrt{\frac{lnn_p}{n_i}})$$
	* $v_i$ is the value of the node $i$ (e.g. $\bar{x}$, from the perspective form the player to move!)
	* $n_i$ is the visit count of $I$
	* $n_p$ is the visit count of $p$
	* $C$ is a coefficient (0.4-0.8) to balance exploitation and exploration 

**Play-out**
* Aka roll-out or simulation
* Plays nearly-random moves (default)  
* Moves are played until the end of the game  
* Quite weak on its own: “Battle of the Apes”  
* Uses heuristics  
	- Bias the moves to good ones (play-out policy)  
	- Early termination of the play-out

**Expansion**
* Standard: first node encountered in the play-out added to the tree  
* The tree grows progressively  
* Other expansion schemes possible to control memory consumption

**Backpropagation**
* The result of a playout is backpropagated from the leaf node, through the previously traversed path (+1 win, 0.5 draw, 0 loss)  
* The value v of a node is computed by taking the average of the results of all simulated games made through this node

