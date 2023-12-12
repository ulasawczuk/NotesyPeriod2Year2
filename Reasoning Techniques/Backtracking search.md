Let’s solve the problem of $𝑛!𝑑^n$ leaves:
* Variable assignments are commutative, i.e.,  
	\[𝑊𝐴 = 𝑟𝑒𝑑 then 𝑁𝑇 = 𝑔𝑟𝑒𝑒𝑛] same as  
	\[𝑁𝑇 = 𝑔𝑟𝑒𝑒𝑛 then 𝑊𝐴 = 𝑟𝑒𝑑]  
• Only need to consider assignments to a single variable at each node ⇒ 𝑏 = 𝑑 and there are $𝑑^n$ leaves
the order assignements doesn't matter at the same depth we just assume some order

Depth-first search for CSPs with single-variable assignments is called **backtracking search**.
Backtracking search is the basic uninformed algorithm for CSPs .
Can solve 𝑛-queens for 𝑛 ≈ 25. !! ;OOO (look simulated annealing)

##### Example

On each level we try all the possible values for a variable. 

![[Screenshot 2023-11-06 at 2.06.22 PM.png|350]]

TODO add code!! from dlsied

##### Improving backtracking efficiency

We don’t need problem-specific knowledge to improve efficiency.  
**General-purpose** methods can give huge gains in speed.

We can improve efficiency answering the following questions:  
1. Can we detect inevitable failure early?  
2. Which variable should be assigned next?  
3. In what order should its values be tried?  
4. Can we take advantage of problem structure?

**Can we detect inevitable failure early?** 

*Forward checking:*  
• Whenever a value is assigned to a variable, values that are now illegal for other variables are removed  
• Terminate search when any variable has no legal values  
• This is inference in CSPs!

*Example*
![[Screenshot 2023-11-06 at 2.16.22 PM.png|300]]
Keep track of remaining legal values for unassigned variables. Terminate search when any variable has no legal values.
If WA has red then we remove red from NT and SA. (red is not legal value). Assign blue to NT and green to Q. Now SA is an empty set, we got ourselves into a corner :((

**Forward checking** propagates information from assigned to unassigned  
variables, but doesn't provide early detection for all failures!
*Can you see a failure that could be detected earlier?*
When we assign green to Q, we see NT and SA are neighbouring and both blue so fail:(

![[Screenshot 2023-11-06 at 2.18.55 PM.png|300]]
Constraint propagation repeatedly enforces constraints locally.

**Arc consistency**: the simplest form of propagation makes each arc consistent  
The arc 𝑋 → 𝑌 is consistent **iff** for every value of 𝑋 there is some allowed value of 𝑌.
![[Screenshot 2023-11-06 at 2.20.38 PM.png|350]]

![[Screenshot 2023-11-06 at 2.21.19 PM.png|350]]
Check all the arcs (arrows), remove blue from V (cause of SA), remove blue from NSW (SA), red from V, suddenly we need to remove blue from NT :0 failure!
![[Screenshot 2023-11-06 at 2.24.10 PM.png|350]]
Detects failure earlier than forward checking.

**Important:**  
* If 𝑌 loses a value, neighbours of 𝑌 need to be rechecked
* Arc consistency detects failure earlier than forward checking  
* Can be run as a preprocessor or after each assignment  
* Prunes a lot, BUT each step takes longer

```matlab
function BACKTRACKING -SEARCH (csp) returns solution/failure  
	return BACKTRACK({}, csp)
```
```matlab
function BACKTRACK(assignment, csp) returns solution/failure  
	if assignment is complete then return assignment  
	var ← SELECT-UNASSIGNED-VARIABLE (csp, assignment)
	for each value in ORDER-DOMAIN-VALUES(var, assignment, csp) do  
		if value is consistent with assignment then  
		add {var = value} to assignment  
		result ← BACKTRACK(assignment, csp)  
		if result ≠ failure then return result  
		remove {var = value} from assignment  
	return failure  
```

**Which variable should be assigned next?**

*Minimum remaining values (MRV):* choose the variable with the fewest legal values  

![[Screenshot 2023-11-06 at 2.28.47 PM.png|350]]
This heuristics reduces the branching factor!

**Tie-breaker among MRV variables** 
*Degree heuristic:* choose the variable with the most constraints on remaining  
variables
![[Screenshot 2023-11-06 at 2.45.18 PM.png|350]]
First we check the number of available values, if we have a tie then we look at the degree.

**In what order should its values be tried?**

Given a variable, choose the *least constraining value*:  
the one that rules out the fewest values in the remaining variables  
![[Screenshot 2023-11-06 at 2.47.23 PM.png|350]]
Combining these heuristics makes 1000-queens feasible! :O

**Can we take advantage of problem structure?**

Tasmania and mainland are *independent subproblems*  
Identifiable as *connected components* of constraint graph
![[Screenshot 2023-11-06 at 2.48.51 PM.png|300]]

* Worst case solution cost of a problem with 𝑛 variables and domain size 𝑑 is $O(d^n)$  
* Suppose the problem can be divided in subproblems, each with 𝑐 variables out of 𝑛 total
* Worst-case solution cost when dividing in subproblems is $O(\frac{n}{c}d^c)$, linear in 𝑛  

*Example*: 𝑛 = 80, 𝑑 = 2, 𝑐 = 20  
$2^80$ = 4 billion years at 10 million nodes/sec  
$4*2^{20}$ = 0.4 seconds at 10 million nodes/sec

*Tree-structered CSPs*

*Theorem*: f the constraint graph has no loops, the CSP can be solved in $O(nd^2)$ time.

Compare to general CSPs, where worst-case time is $O(d^n)$. This property also applies to logical and probabilistic reasoning (later): an important example of the relation between syntactic restrictions and the complexity of reasoning.

*Algorithm for tree-structured CSPs:*
1. Choose a variable as root, order variables from root to leaves such that every node's parent precedes it in the ordering (topological sort)

![[Screenshot 2023-11-06 at 2.53.23 PM.png|400]]

2. For 𝑗 from 𝑛 down to 2, apply ($O(n)$) REVISE (𝑃𝑎𝑟𝑒𝑛𝑡($X_j$), $X_j$) ($O(d^2)$)
3. For 𝑗 from 1 to 𝑛, assign $X_j$ consistently with 𝑃𝑎𝑟𝑒𝑛𝑡($X_j$)

Cost of the algorithm $O(nd^2)$

*Nearly tree-structered CSPs*

![[Screenshot 2023-11-06 at 4.38.37 PM.png|400]]

*Conditioning*: instantiate a variable, prune its neighbours' domain
*Cutset conditioning*: instantiate (in all ways) a set of variables such that the remaining constraint graph is a tree

*Cutset conditioning approach*
1. Choose a subset $S$ of the CSP variables that, when removed, transform the constraint graph into a tree. $S$ is called **cycle cutset**
2. For each possible assignment to variables in $S$ that satisfies all constraint on $S$:
	1. Remove from domain of remaining variables the values inconsistent with assignment of $S$
	2. Solve remaining CSP with the algorithm for tree-structured CSPs
	3. If a solution is found, return it together with the current assignment of variables in $S$
Cost of the algorithm: $O(d^c(n-c)d^2)$
$c =$ cycle cutset size,  $d =$ variable domain size, $n =$ tot. num. variables
##### [[Local search]] for CSPs

[[obsidian-vault/Hill-climbing]] and [[obsidian-vault/Simulated annealing]] typically work with “complete” states, i.e., all variables assigned.

Applying local search to CSPs:

Backtracking | Local search
----|----
(Incomplete) variable assignment with satisfied constraints | Complete variable assignment with unsatisfied constraints 
Extend variable assignment | Change variable assignment
Operators assign variable values | Operators reassign variable values
Frontier with states to expand | No frontier! Only one state

**Algorithm**:
While CSP not solved:  
1. *Variable selection:* randomly select any conflicted variable  
2. *Value selection* by min-conflicts heuristic:  
	1. choose value that violates the fewest constraints  
	2. i.e., hill-climbing with ℎ(𝑛) = total number of violated constraints

**Example**: n-queens :)

![[Screenshot 2023-11-06 at 3.03.12 PM.png|350]]

*States:* 4 queens in 4 columns (44 = 256 states)  
*Operators:* move queen in column  
*Goal test:* no attacks  
*Evaluation:* ℎ(𝑛) = number of attacks

**Performance of min-conflicts**
Given a random initial state, can solve $n$-queens in almost constant time for arbitrary $n$ with high probability (e.g., $n = 10^7$)

The same appears to be true for any randomly-generated CSP, except in a narrow range of the following ratio:
![[Screenshot 2023-11-06 at 4.21.48 PM.png|300]]

