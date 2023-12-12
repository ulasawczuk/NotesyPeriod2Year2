TODO add studysrive notes!!!!

Problem with a specific state, specific evaluation, specific successor:)))
Standard search problem: *state* is a "black box" (any data structure that supports goal test, evaluation, successor), this is what interests us
**State** is defined by:
* a set of variables $X = {X_1,..., X_n}$
* a set of domains $D = {D_1,..., D_n}$, one for each variable
**Goal test** is a set of constraints $C$ specifying allowable combinations of values for subsets of variables.
Simple example of a formal representation language 9a language we use to specify the goal).
Allows useful general-purpose algorithms with more power than standard search algorithms.
##### CSP examples

**Sudoku**
![[Screenshot 2023-11-06 at 1.33.14 PM.png|350]]
State - current state of the board
Goal test - rules of sudoku

**Map colouring**
![[Screenshot 2023-11-06 at 1.40.37 PM.png|350]]
We want to colour the map. We can easily specify the constraint problem. They must have different colours. Every pair of variables needs to be in a set and not be equal or WA /= NT, WA =/ SA (for the exam how to write it)
![[Screenshot 2023-11-06 at 1.41.58 PM.png|350]]

**Constraint graph**
Just put problem into graph ;|
**Binary CSP**: each constraint relates at most two variables
**Constraint graph**: nodes are variables, arcs show constraints
![[Screenshot 2023-11-06 at 1.43.49 PM.png|350]]
General-purpose CSP algorithms use the graph structure to speed up search.  
E.g., Tasmania is an independent subproblem!

##### Varieties of CPSs

**Discrete variables**
* Finite domains; 𝑛 variables, domain size 𝑑 ⇒ $𝑂(𝑑^n)$ complete assignments
	* e.g., Boolean CSPs, incl. Boolean satisfiability (NP-complete) (boolean satis = whether formula is satisfiable)
* Infinite domains (integers, strings, etc.)
	* e.g., job scheduling, variables are start/end days for each job  
	* cannot enumerate all allowed combinations of values ⇒ need a constraint language, e.g., $𝑆𝑡𝑎𝑟𝑡𝐽𝑜𝑏_1$ + 5 ≤ $𝑆𝑡𝑎𝑟𝑡𝐽𝑜𝑏_3$
	* linear constraints solvable, nonlinear undecidable
	
**Continuous variables**
* infinite ofc
* e.g., start/end times for Hubble Telescope observations  
* linear constraints solvable in polynomial time by Linear Programming methods

##### Variates of constraints

**Unary** constraints involve a single variable,  
e.g., 𝑆𝐴 ≠ 𝑔𝑟𝑒𝑒𝑛  
**Binary** constraints involve pairs of variables,  
e.g., 𝑆𝐴 ≠ 𝑊𝐴  
**Higher-order** constraints involve 3 or more variables,  
e.g., cryptarithmetic column constraints  

**Preferences** (soft constraints), e.g., 𝑟𝑒𝑑 is better than 𝑔𝑟𝑒𝑒𝑛 often  
representable by a cost for each variable assignment → constrained  
optimization problems, we just prefer one state over the other and look fot the best one

**Example cryptarithmetic**
![[Screenshot 2023-11-06 at 1.50.59 PM.png|350]]
We need the auxilary variables to represents digits. Later on alg to solve this.
The squares tie the circles together, connect the constraints (R, O, $X_1$).

##### How can we solve CSP?
A CSP can be solved using **search** + **inference**.
Inference in CSPs is called constraint propagation ⇒ using constraints to reduce the number of legal values for a variable.

**Variables:** 𝑋, 𝑌  
**Domains:** $𝐷_X = 𝐷_Y$ = {0,1,2,3,4,5,6,7,8,9}  
**Constraint:** 𝑌 = $𝑋^2$ , or explicitly (𝑋, 𝑌) belong to {(0,0), (1, 1), (2,4), (3,9)}  
**Domains after inference:** $𝐷_X$ = {0,1,2,3} ,  $𝐷_Y$ = {0,1,4,9}
Propagate the constraints into values.

Constraint propagation can be performed before search, as preprocessing step, or **interleaved** with search.
##### Standard search formulation (incremental)

How to use search to solve a CSP: let’s start with the straightforward, dumb approach, then fix it. 
States are defined by the values assigned so far:
* **Initial state?** the empty assignment, {}  
* **Successor function?** assign a value to an unassigned variable that does not conflict with current assignment.  
	⇒ fail if no legal assignments  
* **Goal test?** the current assignment is complete
##### Pros and cons

1. The formulation is the same for all CSPs!  :D
2. Every solution appears at depth 𝑛 with 𝑛 variables  
	⇒ use depth-first search  
3. Path is irrelevant, so can also use complete-state formulation  
4. Branching factor $𝑏 = (𝑛 − 𝑙)𝑑$ at depth $𝑙$, hence $𝑛!𝑑^n$ leaves!!!! :((

Depth | Branching factor
----|----
0 | $nd$
1 | $(n-1)d$
2 | $(n-2)d$
... | ...
l | $(n-l)d$
... | ...
n-1 | $d$
Leaves: $𝑛𝑑× (𝑛 − 1) 𝑑× (𝑛 − 2) 𝑑× ⋯× (𝑛 − 𝑙) 𝑑  × ⋯×𝑑 = 𝑛!𝑑^n$

How to decrease the branching factor??
[[Backtracking search]]

##### Summary
1. CSPs are special kind of problem:
	* states defined by values of a fixed set of variables
	* goal test defined by constraints on variable values
2. Basic approach:
	* Backtracking = depth-first search with one variable assigned per node
3. Improvements:
	* Variable ordering and value selection heuristics help significantly
	* Forward checking prevents assignments later failure
	* Constraint propagation (e.g. arc consistency) does additional work to constrain values and detect inconsistencies
	* The CSP representation allows analysis of problem structure
	* Tree-structured CSPs can be solved in linear time
4. Iterative min-conflicts is usually effective in practice