
TODO add probability recap

----

#### Probability recap

<font color="#76923c">Joint probability distribution</font> for a set of random variables gives the probability of every atomic  
event on those random variables (i.e., every sample point).
$𝑋, 𝑌, ... , 𝑍$ are random variables with $𝑚, 𝑛, ... , 𝑝$ possible values respectively.

> With the joint probability distribution we can compute the probability of any event, identified by a proposition over the considered random variables

$𝐗$= set of all random variables that define the sample space W  
$𝐘$= set of random variables in the proposition that defines a particular event  
$𝐇= 𝐗 − 𝐘$ = set of random variables not part of the definition of the event

$$P(Y=y) = \sum_hP(Y=y, H=h)$$
$$P(Y_1=y_1,...,Y_n=y_n)= \sum_{h_1,...,h_m}P(Y_1=y_1,...,Y_n=y_n, H_1=h_1,...,H_m=h_m)$$
**Example**
𝐗 = {𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒, 𝐶𝑎𝑣𝑖𝑡𝑦}
𝐘 = {𝐶𝑎𝑣𝑖𝑡𝑦}  
𝐇 = 𝐗 − 𝐘 = {𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒}
$$P(Cavity=true) = \sum_{toothache}P(Cavity=true, toothache)$$$$P(Cavity = true) = P(Cavity = true, Toothache = true)+P(Cavity = true, Toothache =false)$$
##### Conditional probabilities

$𝐗$= set of all random variables that define the sample space W  
$𝒀$= set of random variables in the proposition that defines a particular  
event (query)  
$𝐄$= set of random variables not in the proposition that defines a particular  
event, but for which values 𝐞 are known (evidence)  
$𝐇= 𝐗 − 𝐘 − 𝐄$= set of remaining random variables for which we don’t  
know the values (hidden variables)
$$P(Y|E =e)=\alpha P(Y,E=e)=\alpha \sum_hP(Y,E=e,H=h)$$**Example**
𝐗 = {𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒, 𝐶𝑎𝑣𝑖𝑡𝑦, 𝐶𝑎𝑡𝑐ℎ}
𝐘 = {𝐶𝑎𝑣𝑖𝑡𝑦}  
𝐄 = 𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒 ; 𝐞 = {𝑡𝑟𝑢𝑒}  
𝐇 = 𝐗 − 𝐘 − 𝐄 = {𝐶𝑎𝑡𝑐ℎ}
$$P(𝐶𝑎𝑣𝑖𝑡𝑦|𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒) = 𝑡𝑟𝑢𝑒 = 𝛼𝐏(𝐶𝑎𝑣𝑖𝑡𝑦, 𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒= 𝑡𝑟𝑢𝑒 )= 𝛼\sum_{Catch}𝐏(𝐶𝑎𝑣𝑖𝑡𝑦, 𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒 = 𝑡𝑟𝑢𝑒, 𝐶𝑎𝑡𝑐ℎ)=  
= a𝐏 (𝐶𝑎𝑣𝑖𝑡𝑦, 𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒 = 𝑡𝑟𝑢𝑒, 𝐶𝑎𝑡𝑐ℎ = 𝑡𝑟𝑢𝑒) +  
𝐏(𝐶𝑎𝑣𝑖𝑡𝑦, 𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒 = 𝑡𝑟𝑢𝑒, 𝐶𝑎𝑡𝑐ℎ = 𝑓𝑎𝑙𝑠𝑒))$$

##### Independence
$$P(A|B) = P(A) or P(B|A)= P(B) or P(A,B)=P(A)*P(B)$$
##### Conditional independence
$A$ is conditionally independent of $C$ given $B$.
- $P(A|B,C) = P(A|B)$
- $P(C|A,B) = P(C|B)$
- $P(A,C|B) = P(A|B)P(C|B)$

We can use <font color="#76923c">chain rule</font> to represent joint probability distributions.  
Chain rule is derived by successive application of product rule.

---
#### Bayesian Networks

> A simple, graphical notation for conditional independence assertions and hence for compact specification of full joint distributions.

Syntax:
- a set of nodes, one per variable
- directed links with no directed cycles $\rightarrow$ directed, acyclic graph, (link ~ 'directly' influences)
- a conditional distribution for each node given its parents:
	- $P(X_i|Parents(X_i))$

In the simplest case, conditional distribution is represented as a <font color="#76923c">conditional probability table (CPT)</font> giving the distribution over $𝑋_i$ for each combination of parent values.

----
##### Example

> **1**

Topology of network encodes conditional independence assertions:

![[Screenshot 2023-12-04 at 2.00.09 PM.png|300]]

𝑊𝑒𝑎𝑡ℎ𝑒𝑟 is independent of the other variables.
𝑇𝑜𝑜𝑡ℎ𝑎𝑐ℎ𝑒 and 𝐶𝑎𝑡𝑐ℎ are conditionally independent given 𝐶𝑎𝑣𝑖𝑡𝑦.

>**2**

I'm at work, neighbour John calls to say my alarm is ringing, but neighbour Mary doesn’t call. Sometimes alarm is set off by minor earthquakes. Is there a burglar?

<u>Variables</u>: 𝐵𝑢𝑟𝑔𝑙𝑎𝑟, 𝐸𝑎𝑟𝑡ℎ𝑞𝑢𝑎𝑘𝑒, 𝐴𝑙𝑎𝑟𝑚, 𝐽𝑜ℎ𝑛𝐶𝑎𝑙𝑙𝑠, 𝑀𝑎𝑟𝑦𝐶𝑎𝑙𝑙𝑠  

Network topology reflects “causal” knowledge:  
- A burglar can set the alarm off  
- An earthquake can set the alarm off  
- The alarm can cause Mary to call  
- The alarm can cause John to call  

![[Screenshot 2023-12-04 at 2.02.33 PM.png|350]]

Laziness + ignorance cause some factors to not be modeled as nodes, but they are implicitly summarized in the uncertainty associated with links. E.g. John sometimes confuses the phone ringing with the alarm.

----
#### Compactness

> A <font color="#76923c">CPT</font> for Boolean $𝑋_i$ with 𝑘 Boolean parents has $2^k$ rows for the combinations of parent values.

Each row requires one number 𝑝 for $𝑋_i$ = 𝑡𝑟𝑢𝑒 (the number for $𝑋_i$ = 𝑓𝑎𝑙𝑠𝑒 is just 1 − 𝑝)
If each variable has no more than 𝑘 parents, the complete network requires  $𝑂(𝑛 *2^k)$ numbers for 𝑛 vars.
I.e., grows linearly with 𝑛, vs. $𝑂(2^n)$ for the full joint distribution.
For burglary net, 1 + 1 + 4 + 2 + 2 = 10 numbers (vs. $2^5 − 1 = 31$)

---
#### Semantics

##### Global

<font color="#76923c">Global</font> semantics defines the full joint distribution as the product of the local conditional distributions:
$$P(X_1,...,X_n)= \Pi_{i=1}^nP(X_i|Parents(X_i))$$
$\rightarrow$ a Bayesian Network can answer any query!

**Example**

$P(j\wedge m\wedge a\wedge \neg b\wedge \neg e)= P(j|a)P(m|a)P(a|\neg b,\neg e)P(\neg b)P(\neg e)= 0.9 ×0.7×0.001×0.999×0.998\approx 0.00063$

![[Screenshot 2023-12-04 at 2.08.32 PM.png|350]]

##### Local

<font color="#76923c">Local</font> semantics: each node is independent of its nondescendants given its parents.

![[Screenshot 2023-12-04 at 2.21.19 PM.png|300]]

- descendant = child node or descendant of child node  
- nondescendant = any node that is not a descendant  

- $B$ independent of $E$ given $\emptyset$
	- B is unconditionally independent of E
- $E$ independent of $B$ given $\emptyset$
	- E is unconditionally independent of B
- $J$ independent of {$B,E, M$} given {$A$}
	- Also: 𝐽 independent of 𝐵 given 𝐴,  
	- 𝐽 independent of 𝐸 given 𝐴, etc
- $M$ independent of {$B,E, J$} given {$A$}
- $A$ independent of..?

![[Screenshot 2023-12-04 at 2.25.07 PM.png|250]]

----
#### Markov's blanket

Another independence property: each node is conditionally independent of all others given its Markov blanket: parents + children + children’s parents.

![[Screenshot 2023-12-04 at 2.29.33 PM.png|300]]

---
#### Constructing Bayesian Networks

Need a method such that a series of locally testable assertions of conditional independence guarantees the required global semantics.
1. Choose an ordering of variables $𝑋_1 , ... , 𝑋_n$
2. For 𝑖 = 1 to 𝑛
	1. add $𝑋_i$ to the network
		1. select parents from $𝑋_1 , ... , 𝑋_{i-1}$ such that $P(X_i|Parents(X_i))=P(X_i|X_1,...,X_{i=1})$

This choice of parents guarantees the global semantics:
$P(X_1,...,X_n)=\Pi_{i=1}^nP(X_i|X_1,...,X_{i-1})=\Pi_{i=1}^nP(X_i|Parents(X_i))$

**Example**
Suppose we choose the ordering $M,J,A,B,E$
$P(J|M)=P(J)$ ? no
$P(A|J,M)=P(A|J)?P(A|J,M)=P(A)$ ? no
$P(B|A,J,M)=P(B|A)$ ? yes
$P(B|A,J,M)=P(B)$ ? no
$P(E|B,A,J,M)=P(E|A)$ ? no
$P(E|B,A,J,M) = P(E|A,B)$ ? yes

![[Screenshot 2023-12-04 at 5.01.51 PM.png|200]]

Deciding conditional independence is hard in noncausal directions  
Causal models and conditional independence seem hardwired for humans!  
Assessing conditional probabilities is hard in noncausal directions  
Network is less compact: 1 + 2 + 4 + 2 + 4 = 13 numbers needed

---
#### Compact conditional distributions

CPT grows exponentially with number of parents  
CPT becomes infinite with continuous-valued parent or child

Solution: <font color="#76923c">canonical</font> distributions that are defined compactly

<font color="#76923c">Deterministic</font> nodes are the simplest case:  
𝑋 = 𝑓(𝑃𝑎𝑟𝑒𝑛𝑡𝑠(𝑋)) for some function 𝑓  

E.g., Boolean functions  
𝑁𝑜𝑟𝑡ℎ𝐴𝑚𝑒𝑟𝑖𝑐𝑎𝑛 $\leftrightarrow$ 𝐶𝑎𝑛𝑎𝑑𝑖𝑎𝑛 $\leftrightarrow$  𝑈𝑆 $\leftrightarrow$ 𝑀𝑒𝑥𝑖𝑐𝑎𝑛  

E.g., numerical relationships among continuous variables  
$\frac{𝜕𝐿𝑒𝑣𝑒𝑙}{𝜕𝑡} = 𝑖𝑛𝑓𝑙𝑜𝑤 + 𝑝𝑟𝑒𝑐𝑖𝑝𝑖𝑡𝑎𝑡𝑖𝑜𝑛 − 𝑜𝑢𝑡𝑓𝑙𝑜𝑤 − 𝑒𝑣𝑎𝑝𝑜𝑟𝑎𝑡𝑖𝑜𝑛$

Noisy-OR distributions model multiple causes  
1. Parents $𝑈_1, ... ,U_k$ include all causes (can add leak node)  
2. Independent failure probability $q_i$ for each cause alone
$\rightarrow$ $P(x_i|parents(X_i))=1-\Pi_{j:X_j=true\in parents(X_i)}q_j$

![[Screenshot 2023-12-04 at 5.12.01 PM.png|300]]
Number of parameters <font color="#76923c">linear</font> in number of parents

---
#### Hybrid (discrete+continuous) networks

Discrete: 𝑆𝑢𝑏𝑠𝑖𝑑𝑦? and 𝐵𝑢𝑦𝑠?  
Continuous: 𝐻𝑎𝑟𝑣𝑒𝑠𝑡 and 𝐶𝑜𝑠𝑡

![[Screenshot 2023-12-04 at 5.14.07 PM.png|200]]

> How to deal with this?  

<u>Option 1</u>: discretization – possibly large errors, large CPTs  
<u>Option 2:</u> define standard families of probability density functions with finite number of parameters, e.g. Gaussian distribution  

For hybrid nets we need to specify new kinds of conditional distr.:  
1) Continuous variable, discrete + continuous parents (e.g., 𝐶𝑜𝑠𝑡)  
2) Discrete variable, continuous parents (e.g., 𝐵𝑢𝑦𝑠?)

1. **Continuous child variables:**

For each possible assignment to discrete parents (i.e. 𝑆𝑢𝑏𝑠𝑖𝑑𝑦): need one <font color="#76923c">conditional</font>  
density function for child variable (i.e. 𝐶𝑜𝑠𝑡) given continuous parents (i.e. 𝐻𝑎𝑟𝑣𝑒𝑠𝑡).

2. **Discrete variables with continuous parents:**

Probability of 𝐵𝑢𝑦𝑠? given 𝐶𝑜𝑠𝑡 should be a “soft” threshold:

![[Screenshot 2023-12-04 at 5.18.44 PM.png|300]]

---
#### Summary

- Bayes nets provide a natural representation for (causally induced) conditional  independence  
- Topology + CPTs = compact representation of joint distribution  
- Generally easy for (non)experts to construct  
- Canonical distributions (e.g., noisy-OR) = compact representation of CPTs  
- Continuous variables ⇒ parameterized distributions