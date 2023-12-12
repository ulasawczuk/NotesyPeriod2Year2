Perfect play for deterministic, perfect-information games. 
**Idea:** choose move to position with highest *minimax value* = best achievable payoff  
against optimal play

Optimal play is not the best play! Best play assumes stuff about the oppenent.

**E.g.** 2-ply game:
![[Screenshot 2023-11-07 at 11.11.13 AM.png|400]]

TODO add code!!! silde 7

**Complete:** only if tree is finite (chess has specific rules for this)
**Optimal:** yes, against an optimal opponent, otherwise???
**Time:** $O(b^m)$
**Space:** $O(bm)$ (depth-first exploration)

For chess, b ≈ 35, m ≈ 100 for "reasonable" games -> exact solution completely infeasible, a lot of states ($35^{100}$)
But do we need to explore every path? -> [[Alpha-beta pruning]]
