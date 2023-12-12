
#### Knowledge based agent

TODO add knowledge based agent def

**Simple knowledge based agent**

```
function KB-AGENT(percept) returns an action  
	static: KB, a knowledge base  
		t, a counter, initially 0, indicating time  
	TELL (KB, MAKE-PERCEPT-SENTENCE(percept, t))  
	action ← ASK (KB, MAKE-ACTION -QUERY(t))  
	TELL (KB, MAKE-ACTION -SENTENCE(action, t))  
	t ← t + 1  
	return action
```

TELL function hides details of the inference mechanism. MAKE-ACTION/MAKE-PERCEPT functions hide details of the representation language.

**Example: Wumpus world**

Wumpus World PEAS description:

* Performance measure:  
		gold +1000, death -1000, -1 per step, -10 for using the arrow  
* Environment:  
		4x4 grid of rooms, start in \[1,1], random location of gold and wumpus  
		0.2 probability of pit in a square (except in start position)  
* Actuators: Left turn 90,  Right turn 90, Forward, Shoot, Grab, Climb  
		Moving in square with live wumpus or pit results in death  
		Moving towards a wall has no effect  
		Shooting kills wumpus if you are facing it  
		Shooting uses up the only arrow  
		Grabbing picks up gold if in same square  
		Climbing exits the cave (only from \[1,1])  
* Sensors: Stench, Breeze, Glitter, Bump, Scream  
		Stench in squares orthogonally adjacent to wumpus  
		Breeze in squares orthogonally adjacent to pit  
		Glitter if gold is in the same square  
		Bump when walking into a wall  
		Scream in whole cave when wumpus gets killed
		
![[Screenshot 2023-11-14 at 11.15.14 AM.png|200]]

Wumpus world characterization:

* Fully observable??
	* No - only local perception  
* Deterministic?? 
	* Yes - outcomes exactly specified  
* Episodic?? 
	* No – a decision could affect future decisions  
* Static?? 
	* Yes - Wumpus and Pits do not move  
* Discrete?? 
	* Yes – space, time, percepts and actions  
* Single-agent?? 
	* Yes - Wumpus is essentially a natural feature


Exploring the world

![[Screenshot 2023-11-14 at 11.17.46 AM.png|300]]|![[Screenshot 2023-11-14 at 11.20.38 AM.png|300]]

#### Logic in general

How do we represent the knowledge and perform reasoning with logic?

**Logics** are formal languages for representing information such that conclusions can be drawn  
**Syntax** defines the sentences in the language  
**Semantics** define the “meaning” of sentences;  
	i.e., define truth of a sentence in a world  
E.g., the language of arithmetic  
* Syntax:  
	$𝑥 + 2 \geq 𝑦$ is a sentence; $𝑥2 + 𝑦 >$ is not a sentence  
* Semantics:  
	$𝑥 + 2 ≥ 𝑦$ is true iif the number $𝑥 + 2$ is no less than the number $𝑦$  
	$𝑥 + 2 ≥ 𝑦$ is true in a world where $𝑥 = 7, 𝑦 = 1$  
	$𝑥 + 2 ≥ 𝑦$ is false in a world where $𝑥 = 0; 𝑦 = 6$ 

#### Entailment

Entailment means that a sentence follows logically from another:  
$$𝐾𝐵 |= \alpha$$
Knowledge base 𝐾𝐵 entails sentence $\alpha$ **if and only if**  $\alpha$ is true in all possible worlds where 𝐾𝐵 is true  

E.g., the KB containing “the Giants won” and “the Reds won” entails “Either the Giants won or the Reds won”  
E.g., 𝑥 = 0 entails 𝑥𝑦 = 0  

Entailment is a relationship between sentences (i.e., syntax) that is based on semantics.

#### Models

>“possible worlds” = models

Logicians typically think in terms of models, which are formally structured worlds with respect to which truth can be evaluated.
We say 𝑚 is a model of a sentence $\alpha$ if $\alpha$ is true in 𝑚.

$M(\alpha)$ is the set of all models of $\alpha$
Then $𝐾𝐵 |= \alpha$ **if and only if** $M(KB) \subset M(\alpha)$ 

E.g.  
𝐾𝐵 = Giants won and Reds won  
$\alpha$ = Giants won

---
**Entailment in Wumpus world**

Situation after detecting nothing in (1,1), moving right, breeze in (2,1).
Consider possible models for the question marks assuming only pits:  
3 boolean choices $\rightarrow$ 8 possible models

![[Screenshot 2023-11-14 at 11.33.11 AM.png|200]]

---
#### Inference

>The definition of entailment can be applied to derive conclusions (logical inference).

Entailment = tells us that $\alpha$ is a consequence of 𝐾𝐵  
Inference = procedure that derives $\alpha$ from 𝐾𝐵

Inference: $𝐾𝐵 |−_i \alpha =$ sentence a can be derived from 𝐾𝐵 by inference algorithm 𝑖

**Soundness:** 
𝑖 is sound if whenever $𝐾𝐵 |−_i \alpha$, it is also true that $𝐾𝐵 |= \alpha$  
**Completeness:**  
𝑖 is complete if whenever $𝐾𝐵 |= \alpha$, it is also true that $𝐾𝐵 |−_i \alpha$  

e.g. Model checking is an inference algorithm. It is sound and  
complete when the space of models is finite.

---
#### Knowledge-based agents using propositional (Boolean) logic

##### Propositional logic recap

**Syntax**:
Propositional logic is the simplest logic - illustrates basic ideas 

- The proposition symbols $𝑃_1 , 𝑃_2$ etc. are atomic sentences  
- If $𝑆$ is a sentence, ¬𝑆 is a sentence (negation)  
- If $𝑆_1$ and $𝑆_2$ are sentences, $S_1 \wedge S_2$ is a sentence (conjunction)  
- If $𝑆_1$ and $𝑆_2$ are sentences, $𝑆_1 \vee 𝑆_2$ is a sentence (disjunction)  
- If $𝑆_1$ and $𝑆_2$ are sentences, $𝑆_1 \rightarrow 𝑆_2$ is a sentence (implication)  
- If $𝑆_1$ and $𝑆_2$ are sentences, $𝑆_1 \leftrightarrow 𝑆_2$ is a sentence (biconditional)

**Semantics**:
Each model specifies true/false for each proposition symbol

E.g.
$P_1$ false
$P_2$ false
$P_3$ true
is a model
(With these symbols, 8 possible models, can be enumerated automatically.)  

Rules for evaluating truth with respect to a model $m$:
- $\neg P$ is true iff $P$ is false 
- $P_1 \wedge P_2$ is true iff $P_1$ is true and $P_2$ is true
- $P_1 \vee P_2$ is true iff $P_1$ is true or $P_2$ is true
- $P_1 \rightarrow P_2$ is true iff $P_1$ is false or $P_2$ is true
- $P_1 \rightarrow P_2$ is false iff $P_1$ is true and $P_2$ is false
- $P_1 \leftrightarrow P_2$ is true iff $P_1 \rightarrow P_2$ is true and $P_1 \rightarrow P_2$ is true

**Truth tables**

![[Screenshot 2023-11-18 at 5.11.45 PM.png]]

