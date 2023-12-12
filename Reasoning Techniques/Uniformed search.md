#### Problem solving agents

* Simple reflex agents 
	* if-else statement from outputs
* Model-based reflex agents
	* keeps model of environment in head to decide what to do
* Goal-based agents
	* moves towards a certain goal
* Utility-based agents
	* they can say how good a certain outcome is

#### Environments

| Type 1 | Type 2 | Difference |
| ------|----|----|
| Fully observable | Partially observable | Fully if everything in environment is known by agent |
| Single agent | Multi agent | Single agent if an agent operates by itself |
| Deterministic | Nondeterministic| Deterministic if next stage completely determined by current state and action taken |
| Episodic | Sequential | Episodic if the action in some "part" depends only on the "part"|
| Static | Dynamic | Static if the environment does not change when the agent is deliberating|
| Discrete | Continuous | Discrete if there is a defined, fixed number percepts and actions |
| Known | Unknown | All rules are known, real world is unknown |

#### Problem types

**Single-state problem**
* deterministic, fully observable, known environment
* agent knows exactly which state it will be in; solution is a fixed sequence of actions
**Conformant (sensorless) problem**
* non-observable environment
* agent may have o idea where it is; solution (if any) is a sequence of actions
**Contingency problem**
* nondeterministic and/or partially observable
* percepts provide new information about current state; solution is a *contingent plan* or a policy often interleave search, execution
**Exploration problem**
* unknown state space 
* not in this course :)))

#### Problem solving process

1. Formulate goal
2. Formulate problem
3. Search for solution (= sequence of actions)
4. Execute sequence of actions

**Open-loop problem**: 
Don't look at perceptions after initial state. Determine set of actions at beginning, and follow through without checking environment during actions.
**Closed-loop problem:**
Look at perceptions before each action. Determine next action based of current state/perceptions each time.
(this is open-loop problem solving)

#### Single-state problem formulation

(imagine I wanna be in Bucharest but I'm in Arad:/)
1. Initial state: the starting point 
	* In(Arad)
2. Actions: ACTIONS(x) - set of actions that can be executed in state x
	* e.g., ACTIONS(In(Arad)) = {Go(Sibiu), Go(Timisoara), Go(Zerind)} 
3. Successor function: S(x) - set of action state pair (i.e what each action does)
	* e.g., S(In(Arad)) = {⟨Go(Sibiu), In(Sibiu)⟩, ..., ⟨Go(Zerind), In(Zerind)⟩}
4. Goal test: Explicit - specify state it has to be in, Implicit - specify a condition for the state
	* explicit, e.g., x = In(Bucharest)
	* implicit, e.g., NoDirt(x)
5. Path cost: how much is the cost of getting to a certain state with a specific path 
	* e.g., sum of distances, number of actions executed, etc.
	* $c(x, a, x')$ is the step cost, assumed to be ≥ 0 ($x$, $x’$ = states, $a$ = action))

**State space** is defined by 1, 2 and 3 of the problem. 
**Solution** is a sequence of actions leading from the initial state to a goal state.
**Optimal solution** is a solution with the lowest path cost.

#### Selecting a state space

* Real world is absurdly complex -> state space must be abstracted for problem solving.
* Abstract has to be subset of real.
* (Abstract) state = set of real states
* (Abstract) action = complex combination of real actions
	* e.g., Go(Zerind) represents a complex set of possible routes, detours, rest stops, etc.  
	- For guaranteed realizability, any real state In(Arad) must get to some real state In(Zerind)
* (Abstract) solution = set of real paths that are solutions in the real world
* Each abstract action should be "easier" than the original problem

#### Tree search algorithms

* Offline (open-loop)
* Simulated exploration of state space by generating successors of already explored states
```js
function TreeSearch(problem, strategy){
	initialize the search tree using the initial state of problem
	loop do
		if there are no candidates to expand then
			return failure
		choose a leaf node to expand according to strategy
		if the node contains a goal state then
			return the solution
		else expand the node and add the resulting nodes to the search tree
	end
}
```

**Implementation**

A *State* is a (representation of) a physical configuration.
A *Node* is a data structure constituting part of a search tree. Includes parent, children, depth, path cost $g(x)$.

 ![[Screenshot 2023-11-02 at 7.58.49 PM.png]]

**General tree search**
```js
function TreeSearch(problem){
	frontier <- empty set
	frontier <- INSERT(MAKE-NODE(INITIAL-STATE(probem)), frontier)
	loop do
		if frontier is empty then return failure
		node <- REMOVE-FRONT(frontier)
		if GOAL-TEST(problem, STATE[node]) then return node
		frontier <- INSERTALL(EXPAND(node,problem),frontier)
}
```
```js
function EXPAND(node, problem){
	successors <- empty set
	for each action, state in SUCCESSORFN(problem, STATE[node]) do
		s <- new NODE
		PARENT-NODE[s] <- node
		ACTION[s] <- action
		STATE[s] <- state
		PATH-COST[s] <- PATH-COST[node] + STEP-COST(node, action, s)  
		DEPTH[s] <- DEPTH[node] + 1  
		add s to successors  
	return successors
}
```

**Search strategies**

Defined by picking the order of node expansion
Can be evaluated along 4 dimensions:
* completeness: does it always find a solution if one exists?
* time complexity: number of nodes generated/expanded
* space complexity: maximum number of nodes in memory
* optimally: does it always find a least-cost solution?
Time and space complexity are measured in terms of:
* b: maximum branching factor of the search tree
* d: depth of the least-cost solution
* m: maximum depth of the state space (may be infinity)

#### Uninformed search strategies

* [[Breadth-first search]]
* [[Uniform-cost search]]
* [[Depth-first search]]
* [[Depth-limited search]]
* [[Iterative deepening search]]

**Properties of all algorithms**

Criterion | Breadth-first | Uniform_cost | Depth-first | Depth-limited | Iterative deepening
 ------|----|---|----|----|----
Complete? | yes, if b finite | yes, if b finite and step costs ≥ 𝜀 | no | no, unless $l > d$ | yes, if b is finite
Optimal? | yes, if step costs identical | yes | no | no | yes, if step costs identical
Time | $O(b^d)$ | $O(b^{C*/\epsilon})$ | $O(b^m)$ | $O(b^l)$ | $O(b^d)$  
Space | $O(b^d)$ | $O(b^{C*/\epsilon})$ |$O(bm)$ | $O(bl)$ | $O(bd)$  

Notice that we have linear space!

