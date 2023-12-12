#### Decision Trees for Classification

A decision tree is a tree where:
* Each interior node tests an attribute  
* Each branch corresponds to an attribute value  
* Each leaf node is labelled with a class (class node)

![[Screenshot 2023-11-09 at 12.55.53 PM.png|500]]

```js
function classify(x, node)  
	if node is a classification node then  
		return the class of node;  
	else  
		determine the child of node that match x.  
		return Classify(x, child)
```

**Example**: Tenis data set

![[Screenshot 2023-11-09 at 12.58.06 PM.png|300]]

Decide whether to play tennis today!:  
* Choose the most frequent label $𝑦 \in 𝑌$  
* 5 times “No”, 9 times “Yes”  
* Answer: play tennis today  
Was this decision difficult?  
* Would be easier if the ratio was 0 “No” to 14 “Yes” ?  

>How can we quantify the difficulty of the decision ?

![[Screenshot 2023-11-09 at 12.59.57 PM.png|300]]

---
#### Entropy
[[https://www.youtube.com/watchv=DxL2HoqLbyA&pp=ygUpdGhlIG1vc3QgbWlzdW5kZXJzG9vZCBjb25jZXB0IGluIHBoeXNpY3M%3D]] <- mega cool video

Entropy measures information in a random process.
Axioms of information $𝐼(𝑝) = −l𝑛(𝑝)$:
* An event’s information decreases as it’s probability increases.  
* The occurrence of an event with probability 1 is not informative.  
* The information of $k$ independent events is the sum of their individual information values.

>Entropy is the mean information across events weighted by probabilities.

$$E(P) = \sum_{i \in {1,2,..,k}}P_iI(P_i)$$

**Exercise**: Which colour will be drawn from the box?

1. ![[Screenshot 2023-11-09 at 1.06.19 PM.png|150]]

Colour | Probability | Weighted Information $p*I$
---|---|---
Red|$\frac{12}{15}$ |0.18
Green| $\frac{1}{15}$ | 0.18
Blue |$\frac{2}{15}$ |0.27
Entropy $E$ = 0.63

2. ![[Screenshot 2023-11-09 at 1.08.46 PM.png|150]]

Colour | Probability | Weighted Information $p*I$
---|---|---
Red|$\frac{8}{15}$ |0.34
Green| $\frac{3}{15}$ | 0.32
Blue |$\frac{4}{15}$ |0.35
Entropy $E$ = 1.01

##### Entropy in $Y$

The entropy is high in $Y$, hence the decision whether to play tennis is difficult.
When Y has only 2 possible labels (“yes”,”no”), we can plot entropy like this:

![[Screenshot 2023-11-09 at 1.36.17 PM.png|150]]

When Y has more possible labels, we need a higher dimensional plot.
$$E = -\frac{9}{14}*ln(\frac{9}{14}) - \frac{5}{14}*ln(\frac{5}{14}) = 0.65$$
9 yes and 5 no

---
#### Decision Tree Learning

Iterative dichotomization 3 (ID3) Algorithm:  
1. Assign the “best” attribute A to the current node N.  
2. For each value of A, create a child node for N.  
3. Assign the corresponding training examples to these child nodes.  
4. IF training examples perfectly classified, THEN STOP. 
	ELSE iterate over new child nodes

----
##### Information Gain

>Information Gain is the expected reduction in entropy after partitioning the instances from sample $S$ according to a given attribute.

Information Gain is computed **for each attribute A** .
The attribute with highest gain is considered “best” and used to make a decision at the current node in the tree.

$$Gain(S,A) = E(P^S) -\sum_{v\in Values(A)}\frac{|S_v|}{|S|}E(P^{S_v})$$
where,
* $S$ = sample
* $A$ = attribute
* $E$ = entropy
* $P$ = probability distribution
* $S_v$ = sample $S$ has value $v$ along $A$

---
**For tennis**:

1. Information gain for split by outlook:

![[Screenshot 2023-11-09 at 1.45.34 PM.png|250]]

$$Gain(S, outlook) = E(9 yes, 5 no) - (\frac{5}{14}E(2 yes, 3no) + \frac{5}{14}E(3 yes, 2no)+\frac{4}{14}E(4 yes, 0no))$$
$$= 0.65 -0.24-0.24-0 =0.17$$
2. Information gain for split by temperature:

![[Screenshot 2023-11-09 at 1.51.54 PM.png|250]]

$$Gain(S, temperature) = E(9 yes, 5 no) - (\frac{4}{14}E(2 yes, 2no) + \frac{6}{14}E(4 yes, 2no)+\frac{4}{14}E(3 yes, 1no))$$
$$= 0.65- 0.20-0.27-0.16=0.02$$
3. Information gain for split by humidity

![[Screenshot 2023-11-09 at 1.55.09 PM.png|250]]

$$Gain(S, humidity) = E(9 yes, 5 no) - (\frac{7}{14}E(3 yes, 4no) + \frac{7}{14}E(6 yes, 1no))$$
$$= 0.65-0.35-0.21=0.1$$

4. Information gain for split by wind

![[Screenshot 2023-11-09 at 1.55.55 PM.png|250]]

$$Gain(S, temperature) = E(9 yes, 5 no) - (\frac{8}{14}E(6 yes, 2no) + \frac{6}{14}E(3 yes, 3no))$$
$$=0.65-0.32-0.30=0.03$$

Now we have all of the information gains!!

Outlook | Temperature | Humidity | Wind
-|-|-|-
0.17|0.02|0.1|0.03

As Outlook has the highest gain:
* Split data by outlook  
* Allocate subsets of the data to each branch 
* If a subset is unanimous we have a leaf node  
* Else: we recurse  

![[Screenshot 2023-11-09 at 2.02.03 PM.png|200]]

Next basically we take only the sunny attributes and compute the information gain for each of the next attributes (temperature, humidity and wind). For overcast we don't need to do that as we always play tennis if it's overcast. For rainy we do the same as sunny.

---
##### Continuous Attributes

**Example**: temperature as a number instead of a discrete value
**Two solutions**:
* Pre-discretize
	* Cold if Temperature<70, Mild between 70 and 75, Hot if Temperature>75
* Discretize during tree growing:

		![[Screenshot 2023-11-09 at 2.06.01 PM.png|200]]

How to find the cut-point?

![[Screenshot 2023-11-09 at 2.08.00 PM.png|300]]
![[Screenshot 2023-11-09 at 2.09.13 PM.png|300]]

----
##### Oblique Decision Trees

* Test condition may involve multiple attributes  
* More expressive representation  
* Finding optimal test condition is computationally expensive

![[Screenshot 2023-11-09 at 2.10.40 PM.png|400]]

---
##### Posterior Class Probabilities

If you stop growing the tree before each leaf node is unanimous in terms of $Y$, it makes sense to output class probabilities along with your prediction for the majority class.

![[Screenshot 2023-11-09 at 2.12.24 PM.png|400]]

---
##### Summary of iterative dichotomization (ID3)

>- Determine the attribute with the highest information gain on the training set.  
>- Use this attribute as the root, create a branch for each of the values the attribute can have. 
>- For each branch, repeat the process with subset of the training set that is classified by that branch.  

**Hypothesis Space Search ID3**

![[Screenshot 2023-11-09 at 2.17.11 PM.png|300]]

Hill climbing is a greedy optimization technique in which you improve a current hypothesis $h$ (i.e. model) by taking the current best step.
On a cost landscape defined by all possible hypotheses and their performances you will thus “climb your current hill”.  
Hill-climbing thus results in a locally optimal hypothesis (like $h’$), rather than a globally optimal hypothesis (like $h^*$).

**The evaluation function is the information gain.** 
* ID3 maintains only a single current decision tree. 
* ID3 performs no backtracking in its search. 
* ID3 uses all training instances at each step of the search.

**Inductive Bias in ID3**

* Preference for short trees  
* Preference for trees with high information gain attributes near the root.  
* Bias is a preference to some hypotheses, not a restriction on the hypothesis space.
