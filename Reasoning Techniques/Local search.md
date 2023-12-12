**Local search**:
* [[Hill-climbing]]
* [[Simulated annealing]]

##### Iterative improvement algorithms
In many optimization problems, path is irrelevant; the goal state itself is the solution.(in previous alg the path (e.g order of nodes) were the sol, here no)
Then state space = set of "complete" configurations. (find optimal configuration e.g TSP, or find configuration satisfying constraints e.g timetable). 
In such cases we can use iterative improvement algorithms that keep a single "current" state and try to improve it.
These algorithms have constant space and are suitable for online (input in parts) and offline (whole input at once) search. (online: selection sort, offline: insertion sort)

**Example:**
Travelling salesman problem TSP
Start with any complete tour, perform pairwise exchanges
Situation on the left is more complicated than on the right, the connection is stable on the right which is more optimal for the given state. 

![[Screenshot 2023-11-04 at 4.09.37 PM.png|300]]
Variants of this approach get within 1% of optimal very quickly with thousands of cities.

**Example:**
n-queens
Put $n$ queens on an $n x n$ board with no two queen on the same row, column or diagonal. (cannot attack each other)
Move a queen in the same column to reduce number of conflicts.
Almost always solves n-queens problems almost instantaneously for very large $n$, e.g $n = 10^6$

![[Screenshot 2023-11-04 at 4.13.20 PM.png|350]]
h represents the number of possible attacks, we aim for 0