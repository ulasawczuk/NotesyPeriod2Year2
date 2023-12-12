or gradient ascent/descent
"Like climbing Everest in thick fog with amnesia"

```js
function HILLCLIMBING (problem)  
	inputs: problem, a problem  
	local variables: current, a node 
					 neighbor, a node  
	current ← MAKE-NODE(INITIAL-STATE[problem])  
	loop do  
		neighbor ← a highest-valued successor of current  
		if VALUE[neighbor] ≤ VALUE[current] 
			then return STATE[current]  
		current ← neighbor  
	end
```
returns a state that is a local maximum

* Useful to consider state space landscape
* Random-restart hill climbing overcomes local maxima - trivial, complete
* Random sideways (non-decreasing) moves escape from shoulders, but loop on flat maxima

![[Screenshot 2023-11-04 at 4.21.30 PM.png|400]]