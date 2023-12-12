**Idea:** escape local maxima by allowing some "bad" moves but gradually decrease theirs size and frequency.
We let us achieve the worst situation and just try to improve. Irl annealing is a process of heating up a material to a specific temperature, keep it at it for some time and then gradually decrease the temperature. This often makes the material more workable with.
```js
function SIMULATEDANNEALING(problem, schedule)
	inputs: problem, a problem  
			schedule, a mapping from time to “temperature”  
	local variables: current, a node  
					 next, a node  
					 T, a “temperature” controlling prob of downward steps  
	current ← MAKE-NODE (INITIAL-STATE [problem])  
	for t ← 1 to ∞ do  
		T ← schedule[t]  
		if T = 0 
			then return current  
		next ← a randomly selected successor of current  
		∆E ← VALUE [next] - VALUE[current]  
		if ∆E > 0 then current ← next  
		else current ← next only with probability 𝑛𝑛∆𝐸𝐸𝑇𝑇(e^{delta*E/T})
```
returns a solution state  

**Properties:**
* $T$ decreased slowly enough -> always reach best state $x^*$ 
* Widely used in VLSI layout, airline scheduling etc.
