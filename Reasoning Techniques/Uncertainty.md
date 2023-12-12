
Let action $A_t$ = leave for airport t minutes before flight
Will $A_t$ get me there on time?

**Problems:**
1. partial observability (road state, other drivers’ plans, etc.)
2. noisy sensors (traffic reports)
3. uncertainty in action outcomes (flat tire, etc.)
4. immense complexity of modelling and predicting traffic

Hence a purely logical approach either:
1. risks falsehood: “$A_{25}$ will get me there on time”    OR
2. leads to conclusions that are too weak for decision making: “$A_{25}$ will get me there on time if there’s no accident on the bridge and it doesn’t rain and my tires remain intact etc etc.” à Qualification problem

**Methods for handling uncertainty**

1. Default or nonmonotonic logic:
- Assume my car does not have a flat tire
- Assume $A_{25}$ works unless contradicted by evidence
- Issues: What assumptions are reasonable? How to handle contradiction?
2. Rules with fudge factors:
- $A_{25}$ ↦0.3 AtAirportOnTime
- Sprinkler ↦_0.99 WetGrass
- WetGrass ↦_0.7 Rain
- Issues: Problems with combination, e.g., Sprinkler causes Rain?
3. Probability:
- Given the available evidence, $A_{25}$ will get me there on time with probability 0.04.
- Mahaviracarya (9th C.), Cardamo (1565) theory of gambling

> ! Fuzzy logic handles degree of truth NOT uncertainty e.g., WetGrass is true to degree 0.2.

----
#### Probability

Example: diagnosing toothache with propositional logic

- Toothache ⇒ Cavity – Ok?? No, patient could have abscess, ...
- Toothache ⇒ Cavity and Abscess and… – Ok?? Qualification problem.
- Cavity ⇒ Toothache – Ok?? No, not all cavities cause pain.

Probabilistic assertions summarize effect of
- <font color="#76923c">laziness</font>: failure to enumerate exceptions, qualifications, etc.
- <font color="#76923c">ignorance</font>: lack of relevant facts, initial conditions, etc.

**Subjective or Bayesian probability:**

Probabilities relate propositions to one’s own state of knowledge
e.g., $P(A_{25} |$no reported accidents)=0.06

Probabilities of propositions change with new evidence:
e.g., $P(A_{25} |$no reported accidents, 5am)=0.15

---
#### Making decisions under uncertainty

Suppose I believe the following:

$P(A_{25}$  gets me there on time|…)=0.04
$P(A_{90}$  gets me there on time|…)=0.70
$P(A_{120}$  gets me there on time|…)=0.95
$P(A_{1440}$  gets me there on time|…)=0.9999

Which action to choose?

Depends on my <font color="#76923c">preferences</font> for missing flight vs. airport cuisine, etc.

<font color="#76923c">Utility theory</font> is used to represent and infer preferences
Decision theory = utility theory + probability theory

An agent is <font color="#76923c">rational</font> iff it chooses the action that yields the highest expected utility, averaged over all the possible outcomes of the action $\rightarrow$ <font color="#76923c">Principle of Maximum Expected Utility (MEU)</font>

**Decision theoretic agent**

![[Screenshot 2023-12-01 at 1.48.04 PM.png|400]]

----
#### Bayesian probability

Begin with set $\Omega$ - the <font color="#76923c">sample space</font> (all possible worlds)
e.g., 6 possible rolls of a die, 36 possible rolls of 2 dice, …
$ω∈\Omega$ is a sample point/possible world/atomic event

A <font color="#76923c">probability space </font>or <font color="#76923c">probability model</font> is a sample space with an assignment $P(ω)$ for every $ω∈\Omega$ s.t. $$0 \leq P(\omega) \leq 1$$$$\sum_{\omega}P(\omega)=1$$
e.g., $P(1)=P(2)=P(3)=P(4)=P(5)=P(6)=\frac{1}{6}$.

An <font color="#76923c">event</font> A is any subset of $\Omega$. $$P(A) = \sum_{\omega \in A}P(\omega)$$
E.g., $P(die roll<4)=P(1)+P(2)+P(3) =\frac{1}{6}+\frac{1}{6}+\frac{1}{6}=\frac{1}{2}$

A <font color="#76923c">random variable</font> is a function from sample points to some range, e.g., the reals or Booleans

e.g., Odd:W ® {true,false}.
	   Odd(1)=true.
	   Weather:W : {sunny,rain,cloudy,snow}.
	   Weather($ω_i$)=sunny.

P induces a <font color="#76923c">probability distribution</font> for any random variable
$$X: P(X=x)= \sum_{\omega:X(\omega)=x_i}P(\omega)$$ e.g., $P(Odd=true)=P(1)+P(3)+P(5)=\frac{1}{6}+\frac{1}{6}+\frac{1}{6}=\frac{1}{2}$

**Propositions**
Think of a <font color="#76923c">proposition</font> as the event (set of sample points) where the proposition is true.
Given Boolean random variables A and B:
- event a = set of sample points where A(ω)=true
- event ¬a = set of sample points where A(ω)=false
- event $a \wedge b$ = points where A(ω)=true and B(ω)=true

Often in AI applications, the sample points are defined by the values of a set of random variables, i.e., the sample space is the Cartesian product of the ranges of the variables.
With Boolean variables, sample point = propositional logic model
e.g., A=true, B =false, or $a \wedge \neg b$
Proposition = disjunction of atomic events in which prop. is true.

> Why use probability?

The definitions imply that certain logically related events must have related probabilities
E.g., P($a \wedge b$)=P(a)+P(b)-P($a \wedge b$)

![[Screenshot 2023-12-01 at 2.01.39 PM.png|300]]

---
#### Syntax and semantics

**Syntax for propositions**

<font color="#76923c">Boolean</font> random variables
e.g., Cavity (do I have a cavity?)
Cavity = true is a proposition, also written cavity
Cavity = false is a proposition, also written $\neg$cavity

<font color="#76923c">Discrete</font> random variables (finite or infinite)
e.g., Weather is one of {sunny, rain, cloudy, snow}
Weather = rain is a proposition
Values must be exhaustive and mutually exclusive

<font color="#76923c">Continuous</font> random variables (bounded or unbounded)
e.g., Temp=21.6; also allow, e.g., Temp<22.0.

> Arbitrary Boolean combinations of basic propositions

---
#### Prior probability

<font color="#76923c">Prior</font> or <font color="#76923c">unconditional probabilities</font> of propositions
e.g., P(Cavity=true)=0.2 and P(Weather=sunny)=0.72
correspond to belief prior to arrival of any (new) evidence

<font color="#76923c">Probability distribution</font> gives values for all possible assignments:
P(Weather)={0.72, 0.1, 0.08, 0.1} (normalized, i.e., sums to 1)

<font color="#76923c">Joint probability distribution</font> for a set of random variables gives the probability of every atomic event on those random variables (i.e., every sample point)

P(Weather, Cavity) = a 4×2 matrix of values:
![[Screenshot 2023-12-01 at 2.08.37 PM.png|400]]

> Every question about a domain can be answered by the joint distribution because every event is a sum of sample points

---
#### Conditional probability

<font color="#76923c">Conditional</font> or <font color="#76923c">posterior probabilities</font>
e.g., P(cavity|toothache)=0.8
i.e., given that toothache is all I know

Notation for conditional distributions:
P(Cavity|Toothache) = 2-element vector of 2-element vectors

If we know more, e.g., cavity is also given, then we have
P(cavity|toothache, cavity)=1

Note: the less specific belief r<font color="#76923c">emains valid</font> after more evidence arrives, but is not always useful

New evidence may be irrelevant, allowing simplification, e.g.,
P(cavity|toothache, 49ersWin)=P(cavity|toothache)=0.8
This kind of inference, sanctioned by domain knowledge, is crucial.

**Definition of conditional probability:**
$$P(a|b) = \frac{P(a\wedge b)}{P(b)}$$
if $P(b) \neq 0$

**Product rule** gives an alternative formulation: $$P(a\wedge b) = P(a|b)P(b) = P(b|a)P(a)$$
A general version holds for whole distributions, e.g.,$$P(Weather,Cavity)=P(Weather|Cavity)P(Cavity)$$(View as a 4×2 set of equations, not matrix mult.)

Chain rule is derived by successive application of product rule: $$P(X_1,…,X_n )=P(X_1,…,X_{n-1} )P(X_n |X_1,…,X_{n-1})$$

$$=P(X_1,…,X_{n-2} )P(X_{n-1}│X_1,…,X_{n-2} )P(X_n ┤| X_1,…, X_{n-1})$$
$$=...$$
$$=\Pi_{i=1}^n P(X_i│X_1,…,X_{i-1} )$$

----
#### Inference

Start with full joint distribution:

![[Screenshot 2023-12-01 at 2.17.28 PM.png|400]]

For any proposition $ϕ$, sum the atomic events where ϕ is true:
$P(ϕ)=Ʃ_{ω:ω|=ϕ} P(ω)$

TODO ADD changing slides 

---
#### Independence and Bayes' Rule

**Independence**
A and B are <font color="#76923c">independent</font> iff
$$P(A|B)=P(A)  or  P(B|A)=P(B)  or  P(A,B)=P(A)P(B)$$

![[Screenshot 2023-12-01 at 2.21.42 PM.png|400]]

$P(Toothache,Catch,Cavity, Weather) = P(Toothache, Catch, Cavity)P(Weather)$

32 entries reduced to 12; for n independent coin flips, $2^n\rightarrow n$
Absolute independence is powerful but rare!
Dentistry is a large field with hundreds of variables, none of which are independent. What to do?

**Conditional Independence**

$P(Toothache,Cavity,Catch)$ has $2^3-1=7$ independent entries

If I have a cavity, the probability that the probe catches in it doesn't depend on whether I have a toothache:
1.  $P(catch|toothache, cavity)=P(catch|cavity)$

The same independence holds if I haven't got a cavity:
2. $P(catch|toothache, ¬cavity)=P(catch┤|¬cavity)$

Catch is conditionally independent of Toothache given Cavity:
$P(Catch│Toothache,Cavity)=P(Catch|Cavity)$

Equivalent statements:
$P(Toothache|Catch,Cavity) = P(Toothache|Cavity)$
$P(Toothache,Catch│Cavity)$
$=P(Toothache|Cavity)P(Catch|Cavity)$

Write out full joint distribution using chain rule:

$P(Toothache, Catch, Cavity)$
$= P(Toothache|Catch, Cavity)P(Catch, Cavity)$
$= P(Toothache|Catch, Cavity)P(Catch|Cavity)P(Cavity)$
$= P(Toothache|Cavity)P(Catch|Cavity)P(Cavity)$

i.e., $2+2+1=5$ independent numbers

In most cases, the use of conditional independence reduces the size of the representation of the joint distribution from exponential in n to linear in n.

Conditional independence is our most basic and robust form of knowledge about uncertain environments.

----
#### Bayes' Rule

Product rule $$P(a\wedge b)=P(a│b)P(b)=P(b│a)P(a)$$
⇒ Bayes’ rule $$P(a│b) = \frac{P(b|a)P(a)}{P(b)}$$or in distribution form

$$P(Y|X)=\frac{P(X│Y)P(Y)}{P(X)} =\alpha P(X|Y)P(Y)$$

Useful for assessing <font color="#76923c">diagnostic</font> probability from causal probability:
$P(Cause|Effect)=\frac{P(Effect│Cause)P(Cause)}{P(Effect)}$

E.g., let $M$ be meningitis, $S$ be stiff neck:
$P(m│s)=\frac{P(s│m)P(m)}{P(s)} =\frac{0.8×0.0001}{0.1}=0.0008$

> posterior probability of meningitis still very small!

---
#### Bayes' Rule and conditional independence

What happens when we have 2 or more pieces of evidence?

$P(Cavity|toothache \wedge catch)$
$= \alpha P(toothache \wedge catch|Cavity)P(Cavity)$
$= \alpha P(toothache|Cavity)P(catch|Cavity)P(Cavity)$

This is an example of a <font color="#76923c">naive Bayes</font> model:
$P(Cause,Effect_1,…,Effect_n )$
$=P(Cause) P_i P(Effect_i |Cause)$

![[Screenshot 2023-12-01 at 2.37.26 PM.png|400]]

> The size of representation is linear in n.

----
#### Summary

- Probability is a rigorous formalism for uncertain knowledge
- <font color="#76923c">Joint probability distribution </font>specifies probability of every <font color="#76923c">atomic event</font>
- Queries can be answered by summing over atomic events
- For nontrivial domains, we must find a way to reduce the joint size
- <font color="#76923c">Independence</font> and <font color="#76923c">conditional independence</font> provide the tools

