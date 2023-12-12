Task 1
---
![[Screenshot 2023-11-03 at 1.40.20 PM.png|500]]

Your goal is to navigate a robot out of a 15m ́9m maze. The robot starts in the lower left corner of the maze facing north. You can turn the robot to face north, east, south, or west. You can direct the robot to move forward a certain distance (d), although it will stop before hitting a wall. Note that the robot can move forward any distance as measured by a real-valued number (i.e., not just integers).

1. Formulate this single-state problem (HINT: define a coordinate system for the robot). How large is the state space?
Initial state: starting coordinates x, y (the maze is a Cartesian plane :D), At(x,y)
Actions: At(x,y) = Turn(left), Turn(right), Go(d)
Successor function: pair of each possible action and outcome, {<Turn(left), Facing(west)>, <Turn(right), Facing(east)>, <Go(5), At(x+5,y)/At(x,y+5)>....}
State space is defined by initial state, actions and successor function.

2. In navigating a maze, the only place we need to turn is at the intersection of two or more corridors, or at dead ends. Reformulate this problem using this observation. How large is the state space now?


Task 2
---

![[Screenshot 2023-11-03 at 2.21.30 PM.png|500]]
1. [[Breadth-first search]]
Order of investigated nodes: A, B, C, D ..., J!, ..., R!, ... , Y
*Frontier* added but not investigated: K, L, M, N, O, P, ..., T, U (if we stop at J)

2. [[Depth-first search]]
Order of investigated nodes: A, B, E, L, M, F, N, O, C,..., H, R!, ..., J!, V, W, K, X, Y
*Frontier* added but not investigated: S, I, D (if we stop at R)

3. [[Iterative deepening search]] limit = 2
Order of investigated nodes: A, B, C, D, E, F, G, H, I, J!, K
*Frontier* added but not investigated: K

Task 3
---


