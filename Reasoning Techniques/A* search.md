**Idea:** avoid expanding paths that are already expensive
**Evaluation function:** $$f(n) = g(n) + h(n)$$
where:
**$g(n)$** is the cost so far to reach n
$h(n)$ is the estimated cost to goal from n
$f(n)$ is the estimated total cost of path through n to goal

A* search uses an *admissible heuristic*. (a heuristic function is admissible if it never overestimates the cost of reaching the goal)
$h(n)$ ≤ $h^*(n)$ where $h^*(n)$ is the true cost from n.
e.g. $h_{SLD}(n)$ never overestimates the actual road distance.

![[Screenshot 2023-11-03 at 4.46.56 PM.png|500]]

**Complete:** yes, unless there are infinitely many nodes with $f$ ≤ $f(G)$
**Optimal:** yes, cannot expand a frontier until all frontiers with lesser $f(n)$ value are expected
**Time:** exponential in, relative error in $h$ * length of sol., $O(b^d)$
**Space:** keeps all nodes in memory, $O(b^d)$

##### Optimality of A*

**Theorem**:
If $h(n)$ is *admissible* then A* using TREE-SEARCH is optimal.

**Proof**:
Suppose some suboptimal goal $G_2$ has been generated and is in the queue. Let $n$ be an unexpanded node on a shortest path to an optimal goal $G_1$.

![[Screenshot 2023-11-04 at 2.25.11 PM.png|300]]

$f(G_2) = g(G_2)$ since $h(G_2) = 0$, also
$f(G_2) > g(G_1)$ since $G_2$ is suboptimal, and
$f(G_2) \geq f(n)$ since $h$ is admissible.
Since $f(G_2) > f(n)$, A* will never select $G_2$ for expansion.

**Theorem**:
A* expands nodes in order of increasing $f$ value.

**Proof**:
Gradually add "$f$-contours" of nodes (in simple: breadth-first search layers). Contour $i$ has all nodes with $f \leq f_i$ where $f_i \leq f_{i+1}$

![[Screenshot 2023-11-04 at 2.41.51 PM.png|300]]
Basically it means that as we get further form A the $f$ value will ofc increase and that's also the order in which we expand the nodes.
##### Consistency

Most admissible heuristics also have the consistency (monotonicity) property.
A heuristic is consistent if $$h(n) \leq c(n, a, n') + h(n')$$
![[Screenshot 2023-11-04 at 2.33.00 PM.png|150]]

**Theorem**:
If $h(n)$ is *consistent* then A* using GRAPH-SEARCH is optimal.

**Proof**:
A heuristic is consistent if $h(n) \leq c(n, a, n') + h(n')$.
If $h$ is consistent we have $$f(n') = g(n') + h(n')$$$$f(n') = g(n) + c(n, a , n') + h(n')$$$$f(n') \geq g(n) +h(n)$$
$$f(n') = f(n)$$
i.e., $f(n)$ is nondecreasing along any path.

