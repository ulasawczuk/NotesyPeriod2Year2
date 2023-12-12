**Example**
![[Screenshot 2023-11-07 at 11.16.28 AM.png|400]]
Assume we do DFS, we get to 3 (circle), as minimazing player I'll always have at most 3. Now the maximazing player will have at least 3. We go to second branch and we visit 2 (square) so minimazing player has at most 2, now we prune! This means we don't investigate the right siblings of 2 (square) cause the parent will always be at most 2 and the maximazing player which is at least 3 will never choose the branch with at most 2 so we cut the branch. We move onto the next node, we get 14, so at most 14 in the circle. Next we have 5 and 2 which we don't prune as < 14. We are left with 3, at most 2 and 2 in the second layer, the maximazing player chooses 3.
Pruning is dependent on the order of the nodes!!! But we don't know the right order:((((

**Why the name?**
$\alpha$ is the best value (to MAX) found so far off the current path. If $𝑽$ is worse than $\alpha$, MAX will avoid it ⇒ prune that branch. Define $\beta$ similarly for MIN. 
![[Screenshot 2023-11-07 at 11.19.53 AM.png|200]]

TODO add code!!! slide 11

**Properties**
* Pruning *does not* affect the final result
* Good move ordering improves effectiveness of pruning 
* With “perfect ordering”, time complexity = $𝑶(𝒃^{\frac{m}{2}} )$ ⇒ doubles solvable depth
* A simple example of the value of reasoning about which computations are relevant (a form of metareasoning)
* Unfortunately, $35^{50}$ is still impossible! (chess)