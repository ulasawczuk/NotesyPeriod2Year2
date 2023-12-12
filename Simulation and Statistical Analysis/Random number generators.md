
**Random numbers**: Random variates generated from the $U(0,1)$ distribution.

##### Physical methods for generating random numbers
- Well stirred urn (Lotto)  
- Rapidly spinning disk  
- Radiation sources  
- ERNIE  
- Books with tables of random numbers (Rand cooperation)

##### Computer era
- Hook up electronic devices to generate random numbers  
- Read in a table (memory capacity, slow; think tapes)  
- Numeric/arithmetic random number generators

##### Early methods
- Arithmetic methods (1940s and 1950s)  
	- New number determined by one or several preceding numbers according to a fixed formula

**Example:** midsquare method
-  Does not work well at all  
- Degenerates rapidly to zero  
- Not truly random  

---
#### Properties of a "good" random number generator

- Produces numbers that appear to be distributed uniformly on $[0,1]$  
- Produces numbers that do not exhibit any correlation with each other  
- Is fast  
- Does not need much storage memory  
- Can easily produce separate streams of random numbers  
- Can reproduce a given stream of random numbers exactly  
- Produces the same sequence of random numbers for all standard compilers and computers
---
#### Linear Congruential Generators

> A sequence of integers $Z_1, Z_2,...$ defined by the  recursive formula:$$Z_i = (aZ_{i-1}+c)(mod(m))$$

Where,
- Modulus $m$, multiplier $a$, increment $c$ and seed $Z_0$ are nonnegative integers.
- $0 < m$, $a < m$, $c < m$, and $Z_0 < m$

**Looping behaviour:** Random numbers repeat on a cycle, which length is called period of generator.

**Given:**
- m = 24
- a = 11
- c = 17
- $Z_0 = 0$

$Z_i = (aZ_{i-1}+c)(mod(m)) = (11*Z_{i-1}+17)mod(24)$
$Z_1 = (11 *0 +17)mod(24) = 17$
$Z_2 = (11*17+17)mod(24) = 12$
$Z_3 = (11*12+17)mod(24) = 5$
$Z_4 = (11*5+17)mod(24) = 0$

We have a cycle!! (0 -> 17 -> 12 -> 5 -> 0)
With different seeds different cycles, e.g. seed $Z_0 =1$ we have a cycle: 1 -> 4 -> 13 -> 16 -> 1
Preferably you want $m$ to be the length of the cycle (full period).

Thus,
Due to modulus $0 \leq Z_i \leq m-1$, $U(0,1)$ random numbers: $U_i = \frac{Z_i}{m}$

**Two objections**:
1. Not random at all (inherent for pseudorandom numbers) $$Z_i=[a^iZ_0+\frac{c(a^i-1)}{a-1}]mod(m)$$with careful choice of parameters $U_i$’s appear IID U(0,1)
2. $U_i$'s can only take rational values $$0,\frac{1}{m},\frac{2}{m},\frac{3}{m},\frac{4}{m},...,\frac{m-1}{m}$$

TODO add exmaple slide 13/14

- Looping will occur (cycle)  
- Cycle length is period  
- Cycle length depends on seed  
- The period of a good LCG generator should be very large  
	- Often scale of simulation projects large  
	- Full period contributes to uniformity
---
> **THEOREM 7.1**

An LCG has **full period** iff the following three conditions hold  
1. $m$ and $c$ is are relatively prime  
2. If $q$ is a prime number that divides $m$, then $q$ divides $a-1$  
3. If 4 divides $m$, then 4 divides $a-1$
---

**Mixed generators**
- Good choice of $m: m=2^b$?  
	- Where $b$ is the number of binary digits in a word on the computer being used for storage

**Multiplicative generators**
- More widely used than mixed generators  
- $c$ is not needed  
- Choice for $m$: largest prime number that is less than $2^b$

Many experts recommend that LCG’s with modulus $m = 2^{31}$ should no longer be used as the random number generator for general purpose software  
- The period of the generator can be exhausted within a few minutes  
- The generator has relatively poor statistical properties  
- Can bias the results for sample sizes much smaller than the period of the generator
---
**Extensions**

$$Z_i=g(Z_{i-1}, Z_{i-2},..)mod(m)$$
$$Z_i=(aZ_{i-1}^2+bZ_{i-1}+c) mod (m)$$
$$Zi=(a_1Z_{i-1+}a_2Z_{i-2}+...+a_qZ_{i-q})mod (m)$$
Fibonacci generator:$$Z_i=(Z_{i-1}+Z_{i-2})mod (m)$$
Shuffling
Be aware that cycling gets more complicated!

----
#### Feedback Shift Registers

**Bitwise shift**
- Low-level operation  
- In C / C++  
- Left bitwise shift: <<  
- Right bitwise shift: >>  
- Fast operation  
- Also available in languages like Java and Python, though might not be efficient

Shift a bit and create a new one based on the existing ones.


|   $b_{i-5}$   |   $b_{i-4}$   |   $b_{i-3}$   |  $b_{i-2}$    |  $b_{i-1}$    |
|:-----|:-----|:-----|:-----|:-----|

$b_i=(c_1b_{i-1}+c_2b_{i-2}+...+c_qb_{i-q})mod(2)$
$c_k \in${$0,1$}, in general also $c_k ≠0$

$b_i=(b_{i-r}+b_{i-q})mod(2)$
Thus,
$0$ if $b_{i-r}=b_{i-q}$
$1$ if $b_{i-r}≠b_{i-q}$

Obtaining uniform from this: $$u_i=\frac{W_i}{2^L}$$
Where. L = number of bits.

---
#### Testing random number generators

> **Empirical tests**
- Use the generator to generate random numbers  
	- Then examine them statistically  
- Check for uniform distribution  
	- Chi$^2$ test  
- Check for independence  
	- Poker test  
	- Runs (or runs-up) test  
	- Correlation test  
- Not a test for “randomness”, but uniformity or independence

**Disadvantage of empirical tests**

Only a certain segment of the cycle is examined  
-> No information about how generator would perform on other segments of the cycle

**Theoretical tests:** tests how well the generator can perform, based on generator structure and defining constants

- Random numbers fall mainly in the planes  
	- Pairs will be arranged in a lattice fashion along families of parallel lines  
	- Spectral test computes the distance between the planes 
- Large number and variety of tests exist  
	- Controversy over which tests are best  
- Chosen test should be consistent with intended use

![[Screenshot 2023-11-17 at 12.51.33 PM.png|300]]

Three consecutive random numbers plotted, we can see a lot of correlation in the plot, the lines fall into planes.

---
#### Tests specific for independence

##### [[Poker test]]
##### [[Runs test]]

