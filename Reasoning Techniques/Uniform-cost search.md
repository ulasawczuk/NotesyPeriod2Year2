Expand the unexpanded node with the lowest path cost $g(n)$

**Implementation**
*frontier* = queue ordered by path cost, lowest first
Equivalent to [[Breadth-first search]] if step costs are equal

**Complete:** yes if step cost ≥ 𝜀
**Optimal:** yes - nodes expanded in increasing order of $g(n)$
**Time:** $O(b^{1+(C*/\epsilon)})$
**Space:** $O(b^{1+(C*/\epsilon)})$
where $C*$ is the cost of the optimal solution
