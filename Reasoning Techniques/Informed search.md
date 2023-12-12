**Informed search:**
* [[Best-first search]]
* [[A* search]]

##### Admissible heuristics

E.g for the 8-puzzle:

![[Screenshot 2023-11-04 at 2.49.24 PM.png|300]]

$h_1(n)$ = number of misplaced tiles
$h_2(n)$ = total Manhattan distance (i.e number of squares from desired location of each tile)

$h_1(S) = 6$
$h_2(S) = 4+0+3+3+1+0+2+1 = 14$

##### Dominance

If $h_2(n) \geq h_1(n)$ for all $n$ (both admissible) then $h_2$ dominates $h_1$ and is better for search.
If they don't dominate each other, than take the max of all values added together to decide which one is best (want highest values possible).

Typical search costs:

d | IDS | A*($h_1$) | A*($h_2$)
---|--|---|--
14 | 3.473.941 | 539 | 113
24 | 54.000.000.000|39.135 | 1.641

in number of nodes

Given any admissible heuristics $h_a, h_b$,
$h(n) = max(h_a(n), h_b(n))$
is also admissible and dominates $h_a,h_b$

##### Ties

A* expands nodes in order of increasing $f$ value, but what about ties? Break ties based on $g$ value. 
Larger $g$ values mean more accurate information and less heuristic approximation

![[Screenshot 2023-11-04 at 3.09.31 PM.png|400]]

##### Relaxed problems
* Admissible heuristics can be derived from exact solution cost of relaxed version of the problem
* If the rules of the 8-puzzle are relaxed so that a tile can move anywhere, then $h_1(n)$ gives the shortest solution
* If the rules are relaxed so that a tile can move to any adjacent square, then $h_2(n)$ gives the shortest solution
* Key point: the optimal solution cost of a relaxed problem is no greater than the optimal solution cost of the real problem

**Example**:
Travelling salesperson problem (TSP)
Find the shortest tour visiting all cities exactly once.

![[Screenshot 2023-11-04 at 3.54.51 PM.png|200]]
Minimum spanning tree can be computed in $O(n^2)$ and is a lower bound on the shortest (open) tour.

##### Iterative deepening A*
* A* can be memory intensive for large problems
* Iterative deepening A*
* Iterative deepening iterates on a threshold $T$ 
* Search a node as long as $f \leq T$
* Either find a solution, or fail, in which case the threshold is increased and a new depth-first search

##### Summary
* Heuristic functions estimate costs of shortest paths
* Good heuristics can drastically reduce search cost
* Greedy best-first search expands lowest $h$ (incomplete and not always optimal)
* A* search expands lowest $g+ h$ (complete and optimal)
* Admissible heuristics can be derived from exact solution of relaxed problems