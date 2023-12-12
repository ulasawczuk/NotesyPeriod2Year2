
>IF \<conditions> THEN instance belongs to \<class>

* A popular representation for concept definitions:
		Can be more compact and easier to interpret than trees

How can we learn such rules ?  
* By learning trees and converting them to rules  
* With specific rule-learning methods (“sequential covering”)

---
#### Why Decision Rules?

* Decision rules are more compact than decision trees.  
* Decision rules can explain better than decision trees.

**Example**:
Let $X, Y,Z, W \in$ {0,1} and define the rules:
* **if** $X=1$ and $Y=1$ **then** 1
* **if** $Z=1$ and $W=1$ **then** 1
* **otherwise** 0;

![[Screenshot 2023-11-14 at 12.21.36 PM.png|300]]

---

![[Screenshot 2023-11-14 at 12.21.59 PM.png|450]]

> **Decision rules are usually ordered**

* Ordered decision rules are called **decision lists**. 
* Ordered decision rules are logically equivalent to **decision trees**.  
* The order introduces implicitly extra rule conditions.

**if** $X=1$ and $Y=1$ **then** 1|  **if** $X=1$ and $Y=1$ **then** 1
 ---|---
**if** $Z=1$ and $W=1$ **then** 1 | **if** Not($X=1$ and $Y=1$) $Z=1$ and $W=1$ **then** 1
**otherwise** 0; |  **if** Not($X=1$ and $Y=1$) and Not($Z=1$ and $W=1$) **then** 0

---
#### Sequential covering

![[Screenshot 2023-11-14 at 12.35.08 PM.png|500]]

**Learning one rule**

Perform greedy search on literals in a rule’s condition. Can be top-down or bottom-up.

**[[Top-down]]**:
* Start with maximally general rule  
* Add literals one by one  
* Gradually maximize accuracy until only positives are covered

**[[Bottom-up]]**:
* Start with maximally specific rule 
* Remove literals one by one  
* Gradually maximize coverage and stop right before negative instances are covered

Bottom-up | Top-down
---|---
Rules edge with + | Rules edge with -

![[Screenshot 2023-11-14 at 12.58.18 PM.png|200]] | ![[Screenshot 2023-11-14 at 12.59.47 PM.png|190]]

---
#### Learning with exceptions

* The negative class is nested within the cluster of the positive class 
* Regular decision rules would create several bounding boxes  
* Exceptions can simplify the rule set

If $x_1 \in A$ and $x_2 \in B$ Then +

![[Screenshot 2023-11-14 at 1.44.16 PM.png|250]]

If $x_1 \in A$ and $x_2 \in B$ 
	If not ($x_1 \in C$ and $x_2 \in D$)
		Then -
	Else +

![[Screenshot 2023-11-14 at 1.46.11 PM.png|250]]

---
#### Exercise

**Bottom-up**

![[Screenshot 2023-11-14 at 1.51.15 PM.png|300]]

* Find a set of rules that covers all positive instances of Table 1 using the **bottom-up** algorithm.
* Always start with the first positive instance that is not covered. 
* Use accuracy on the covered instances as heuristic to guide the search.

1. Start with the most specific rule that covers $e_1$:
**IF** color = white AND shape = round AND taste = sweet **THEN** pos

2. Search for candidates to generalize this rule:

Canditates:
* **IF** color = white AND shape = round $\rightarrow$ accuracy: 2/2
* **IF** color = white AND taste = sweet $\rightarrow$ accuracy: 1/2
* **IF** shape = round AND taste = sweet $\rightarrow$ accuracy: 1/2

3. Update the first rule
**IF** color = white AND shape = round **THEN** pos

![[Screenshot 2023-11-14 at 1.56.25 PM.png|300]]

* It is not possible to generalize this rule further without covering negative instances.  
* Remove the covered instances  
* Move to second rule

4. Find the most specific rule that covers positive instance $e_3$:
**IF** color = brown AND shape = round AND taste = bitter **THEN** pos **ELSE** neg

* All positive instances are covered, no need to generalize 2nd rule.
* Remove $e_3$
* Terminate with **ELSE** neg.

**IF** color = white AND shape = round **THEN** pos
**IF** color = brown AND shape = round AND taste = bitter **THEN** pos
**ELSE** neg

**Top-down**

* Find a set of rules that covers all positive instances of Table 1 using the **top-down** algorithm.
* Always start with the first positive instance that is not covered.  
* Use accuracy on the covered instances as heuristic to guide the search.

1. Find the most general rule that covers at least  $e_1$, select the one with the highest accuracy:

Candidates:
* **IF** color = white $\rightarrow$ accuracy: 2/3
* **IF** shape = round $\rightarrow$ accuracy: 3/4
* **IF** taste = sweet $\rightarrow$ accuracy: 1/3

We choose shape as it has the highest accuracy.

2. Find the additional literals to make this rule cover less negative instances, select one with the highest accuracy:
**IF** shape = round **THEN** pos

Candidates:
* **IF** color = white $\rightarrow$ accuracy: 2/2
* **IF** taste = sweet $\rightarrow$ accuracy: 1/2

Select color, so
**IF** shape = round AND color = white **THEN** pos

3. Remove covered instances, continue with rule 2

![[Screenshot 2023-11-14 at 2.14.42 PM.png|300]]

4. Construct most general rules that covers at least $e_3$, select most the accurate one;

Candidates:
* **IF** color = brown $\rightarrow$ accuracy: 1/2
* **IF** shape = round $\rightarrow$ accuracy: 1/2
* **IF** taste = bitter $\rightarrow$ accuracy: 1/1

Go with taste.

* All positive instances are covered, no need to specify 2nd rule.  
* Remove $e_3$.  
* Terminate with **ELSE** neg

**IF** shape = round AND color = white **THEN** pos
**IF** taste = bitter **THEN** pos
**ELSE** neg

---
#### Heuristics

Possible evaluation functions for a rule:
* Accuracy: $\frac{n_c}{n}$, where $n_c$ is the number of instances correctly classified by the rule, and $n$ is the number of instances covered by the rule
* m-estimate of accuracy: $\frac{n_c+mp}{n+m}$, where $p$ is the prior probability of the positive class, and $m$ is a weight we choose for this prior
* Entropy

---
#### How to arrange the rules?

1. According to the order they have been learned.  
2. According to their accuracy.  
3. Unordered: devise a strategy how to apply the rules. For example:  
	1. an instance covered by conflicting rules is handled by the rule with higher training accuracy  
	2. if an instance is not covered by any rule, then it is assigned the majority class

##### Approaches to avoiding overfitting

> Pre-pruning:

stop learning the decision rules before they reach the point where they perfectly classify the training data

> Post-pruning:

allow the decision rules to overfit the training data, and then post-prune the rules.

##### Incremental reduced error pruning

1. If Stopping criterion reached: break  
2. Split *Training Set* into *Growing Set* and *Pruning Set*;  
3. Learn rule *R* using *Growing Set*;  
4. Prune the rule *R* using *Pruning Set*;  
5. **if** performance(*R, Growing Set*) > Threshold  
	1. Add *R* to *Set of Learned Rules*
	2. Remove in *Training Set* the instances covered by *R*;  
	3. go to 1;  
6. Do pruning directly after each new rule learned

##### Post-pruning

1. Split instances into *Growing Set* and *Pruning Set*;  
2. Learn set of rules (SR) using *Growing Set*;  
3. Find the best simplification of set of rules (BSR);  
4. **while** Accuracy BSR > Accuracy SR on Pruning Set  
	1. SR = BSR;  
	2. Find the best simplification BSR of SR.  
5. **return** BSR;

**Side-effect of post-pruning**

Depending on your criterion for pruning a rule, the pruned rules might become more general.  Thus more instances are covered by some rules. Other rules might then become obsolete.

![[Screenshot 2023-11-14 at 2.29.49 PM.png|500]]

----
#### Summary

* Decision rules can be easier for human comprehension than decision trees.  
* Decision rules can have simpler decision boundaries than decision trees.  
* Decision rules are learned by sequential covering of the training instances