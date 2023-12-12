
**Games vs search problems**
"Unpredictable" opponent -> solution is a strategy specifying a move for every possible  
opponent reply. In search problems we don't have an opponent and usually we have given time to make a decision.
Time limits -> unlikely to find goal, must approximate.  

Plan of attack:  
*  Computer considers possible lines of play (Babbage, 1846)  
* Algorithm for perfect play (Zermelo, 1912; Von Neumann, 1944)  
* Finite horizon, approximate evaluation (Zuse, 1945; Wiener, 1948; Shannon, 1950)  
* First chess program (on paper) (Turing, 1951)  
* Machine learning to improve evaluation accuracy (Samuel, 1952-57)  
* Pruning to allow deeper search (McCarthy, 1956)  
##### Types of games 

---|Deterministic|Chance
---|----|---
Perfect information| chess, checkers, go, othello|backgammon, monopoly
Imprerfect information | battleship, blind tictactoe| bridge, poker, scrabble

**Game tree** (2-player, deterministic, turns)
![[Screenshot 2023-11-07 at 11.07.41 AM.png|500]]

[[Minimax]]
[[Alpha-beta pruning]]

##### Resource limits 

Standard approach:  
*  Use CUTOFF-TEST instead of TERMINAL-TEST , e.g., depth limit  
*  Use EVAL instead of UTILITY, i.e., **evaluation function** that estimates desirability of position

Suppose we have $100$ seconds, explore $10^4$ nodes/second
* $10^6$ nodes per move ≈ $30^{\frac{8}{2}}$
* $\alpha -\beta$ reaches depth 8 -> pretty good chess program

##### Evaluation functions

![[Screenshot 2023-11-07 at 11.41.05 AM.png|400]]

For chess, typically linear weighted sum of **features**, we take into account what we have and what the opponent has. (i.e number of queens)
$Eval(s) = w_1f_1(s) + w_2f_2(s) + ... + w_nf_n(s)$
e.g. $w_1 =9$ with $f_1(s) =$ (number of white queens) - (number of black queens), etc.

**Digression: exact values don't matter :O**

![[Screenshot 2023-11-07 at 11.45.28 AM.png|400]]
* Behaviour is preserved under any monotonic transformation of EVAL
* Only the order matters: payoff in deterministic games acts as an ordinal utility function

##### Deterministic games in practice

**English checkers**:Chinook ended 40-year-reign of human world champion Marion Tinsley in 1994. Used an endgame database defining perfect play for all positions involving 10 or fewer pieces on the board, a total of 443,748,401,247 positions. Game was solved in 2007

**Chess**: Deep Blue defeated human world champion Gary Kasparov in a six-game match in 1997. Deep Blue searches 200 million positions per second, uses very sophisticated evaluation. Methods for extending some lines of search up to 40 ply.

**Go**: TODO  add go silde 17

What do you do if you don't have time for evaluation function? Or don't have clue what to do?
You're doing something random! You gamble!
[[Monte Carlo Tree Search]]

##### Games of chance

**Backgammon**

![[Screenshot 2023-11-07 at 12.25.51 PM.png|250]]

**Expectimax**

* Chance introduced by dice, card-shuffling
* We go to the node with the highest chance of winning
* Simplified example with coin-flipping:  

![[Screenshot 2023-11-07 at 12.31.31 PM.png|300]]
Diamonds are expected values of the children.

**Algorithms for games of chance**
* EXPECTIMINIMAX (aka EXPECTIMAX) gives perfect play
* Just like MINIMAX, except we must also handle chance nodes:

```matlab
...
if state is a MAX node then  
	return the highest EXPECTIMINIMAX-VALUE of SUCCESSORS(state)  
if state is a MIN node then  
	return the lowest EXPECTIMINIMAX-VALUE of SUCCESSORS(state)  
if state is a chance node then  
	return average of EXPECTIMINIMAX-VALUE of SUCCESSORS(state)
...
```

**Pruning in expectimax trees**

A version of [[Alpha-beta pruning]] is possible:
We introduce intervals based on the values of nodes.

![[Screenshot 2023-11-07 at 12.34.29 PM.png|400]]

More pruning occurs if we can bound the leaf values (values of evaluation function). We bound all of them and then tighten the bounds by ourselves. For this example [-2,2].

![[Screenshot 2023-11-07 at 12.35.48 PM.png|400]]


##### Games of chance in practice 

* Dice rolls increase b: 21 possible rolls with 2 dice  
* Backgammon ≈ 20 legal moves (can be up to 4000) depth 4 = 20 × 21 × 20 3 ≈ 1.2 × 109  
* As depth increases, probability of reaching a given node shrinks ⇒ value of lookahead is diminished
* Pruning is much less effective  
* TDGAMMON uses depth-2 search + very good EVAL (Neural Net) ≈ world-champion level (1995)  

**Digression: Exact values DO matter**

![[Screenshot 2023-11-07 at 12.47.37 PM.png|400]]

* Behaviour is preserved only by positive linear transformation of EVAL
* Don't mess with your evaluation function
* Hence EVAL should be proportional to the expected payoff  

##### Games of imperfect information 

* E.g., card games, where opponent's initial cards are unknown 
* Typically we can calculate a probability for each possible deal  
* Seems just like having one big dice roll at the beginning of the game*  
* Idea: compute the minimax value of each action in each deal, then choose the action with highest expected value over all deals*  
	- Averaging over clairvoyance  
	- AKA Determinisation  
- Special case: if an action is optimal for all deals, it's optimal.*  
- GIB, well-known and strong bridge program, approximates this idea by  
	- generating 100 deals consistent with bidding information  
	- picking the action that wins most tricks on average  

**Example**

Road A leads to a small heap of gold pieces  
Road B leads to a fork:  
	take the left fork and you'll find a mound of jewels;  
	take the right fork and you'll be run over by a bus. 
	 
Road A leads to a small heap of gold pieces  
Road B leads to a fork:  
	take the left fork and you'll be run over by a bus;  
	take the right fork and you'll find a mound of jewels.  
	
Road A leads to a small heap of gold pieces  
Road B leads to a fork:  
	guess correctly and you'll find a mound of jewels;  
	guess incorrectly and you'll be run over by a bus.

**Proper analysis**

Intuition that the value of an action is the average of its values in all actual states is **WRONG**

With partial observability, value of an action depends on the information state or belief  
state the agent is in.
Can generate and search a tree of information states.
Leads to rational behaviors such as  
- Acting to obtain information  
- Signaling to one's partner  
- Acting randomly to minimize information disclosure 

**Summary**

* Games are fun to work on! (and dangerous)
* They illustrate several important points about AI  
	- perfection is unattainable ⇒ must approximate  
	- good idea to think about what to think about  
	- uncertainty constrains the assignment of values to states  
	- optimal decisions depend on information state, not real state
* Games are to AI as grand prix racing is to automobile design  
* More about this in the Master AI Course Intelligent Search & Games