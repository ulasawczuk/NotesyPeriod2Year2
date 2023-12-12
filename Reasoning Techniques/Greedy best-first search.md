* Evaluation function $h(n)$ (heuristic) = estimate of cost from n to the closest goal
* e.g. $h_{SLD}(n)$ = straight-line distance from n to goal
* greedy search expands the node that appears to be the closest to the goal

![[Screenshot 2023-11-03 at 4.28.34 PM.png|500]]![[Screenshot 2023-11-03 at 4.27.53 PM.png|500]]

**Complete:** no, can get stuck in loops (e.g going from Iasi to Fagaras)
**Optimal:** no, (Arad → Sibiu → Rimnicu Vincea → Pitesti → Bucharest) is shorter than (Arad → Sibiu → Fagaras → Bucharest)
**Time:** $O(b^m)$, but with a good heuristic we can improve a lot
**Space:** $O(b^m)$, keeps all the nodes in memory