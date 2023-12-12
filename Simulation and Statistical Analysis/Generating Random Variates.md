
#### Setting

- Distribution already known
- Source of IID $U(0,1)$ random variates available
	- Statistically reliable $U(0,1)$ random number generator must be available
- Considerations
	- Exactness
	- Efficiency
	- Complexity
	- Robustness
---
#### Inverse transformation method

> **Dice throw**

|  Value    |  1    |   2   | 3     |  4    |  5    |  6    |
|:-----|:-----|:-----|:-----|:-----|:-----|:-----|
| Probability     |  $\frac{1}{6}$    |   $\frac{1}{6}$    |   $\frac{1}{6}$    |  $\frac{1}{6}$     |    $\frac{1}{6}$   |   $\frac{1}{6}$|

CDF:

![[Screenshot 2023-11-28 at 11.12.43 AM.png|300]]

> **Continuously**

Suppose we wish to generate a continuous random variate $X$. $X$ has distribution function $F$ that is continuous and strictly increasing when $F(x)$ is between zero and one. 

![[Screenshot 2023-11-28 at 11.15.32 AM.png|350]]

Algorithm:
1. Generate $U \sim U(0,1)$
2. Return $X = F^{-1}(U)$

----
**Example**
Exponential function with rate $\lambda$. Distribution function: $$
 F(x)=\begin{cases} 
      0 & x < 0 \\
      1- e^{-\lambda x} & x \geq 0
   \end{cases}
$$
Find $F^{-1}(U)$.$$U = F(x) = 1- e^{-\lambda x}$$$$1-U = e^{-\lambda x}$$ $$ln(1-U) = -\lambda x$$ $$x = \frac{-ln(1-U)}{\lambda} = \frac{-ln(U)}{\lambda}$$

----
**Truncation easy**

$$f^*(x)=\begin{cases} \frac{f(x)}{F(b)- F(a)} & a \leq x \leq b \\ 0 & else\end{cases}$$

![[Screenshot 2023-11-28 at 11.29.14 AM.png|200]]

----
> **ITM if $X$ is discrete**

Distribution function defined by: $$F(x)= P(X \leq x) = \sum_{x_i\leq x}p(x_i)$$ $$p(x_i) = P(X=x_i)$$
Algoritm:
1. Generate $U \sim U(0,1)$
2. Determine the smallest positive integer, $I$ such that $U \leq F(X_I)$ and return $X=X_I$

![[Screenshot 2023-11-28 at 11.32.42 AM.png|350]]

---
**Example**

Give inverse-transform algorithms for generating from each of the following densities. $$f(x) = \begin{cases} \frac{3x^2}{2} & -1\leq x\leq 1 \\ 0 & otherwise\end{cases}$$
Get $F(x)$: $$F(x) = \begin{cases} 0 & x < -1 \\ \frac{1}{2}x^3 +\frac{1}{2} & -1\leq x\leq 1 \\ 1 & x>1 \end{cases}$$
Now algorithm!: $$U = F(x) = \frac{1}{2}x^3 +\frac{1}{2}$$
$$2U -1 = x^3$$ $$x = \sqrt[3]{2U-1}$$
TODO add exercise 21 on slides

---
#### Composition technique

Applies when the distribution function $F$ can be expressed as a convex combination of other distribution functions. Assume that for all $x$, $F(x)$ can be written as $$F(x) = \sum_{j=1}^\infty p_jF_j(x)$$
where, $$p_j \geq 0, \sum_{j=1}^\infty =1$$
![[Screenshot 2023-11-28 at 11.56.15 AM.png|400]]

![[Screenshot 2023-11-28 at 11.56.58 AM.png|400]]

**Algorithm**

1. Generate a positive random integer $J$ such that: $$P(J=j)=p_j$$
for $j=1,2,...$
2. Return $X$ with distribution $F_J$

----
**Example**
$$f(x) = \begin{cases} \frac{3}{2}x^2 & 0 \leq x \leq 1 \\ \frac{1}{2} & 1 < x \leq \sqrt{3} \\ 0 & else \end{cases}$$
$f_1(x), f_2(x), F_1(x), F_2(x)$:
$$f_1(x) = \begin{cases} 3x^2 & 0\leq x \leq 1 \\ 0 & else \end{cases}$$
$$f_2(x) = \begin{cases} x & 1 < x \leq \sqrt{3} \\ 0 & else \end{cases}$$
$$F_1(x) = \begin{cases} 0 & x<0 \\ x^3 & 0\leq x\leq 1 \\ 1 & x> 1\end{cases}$$
$$F_2(x) = \begin{cases} 0 & x\leq 1 \\ \frac{1}{2}x^2 - \frac{1}{2} & 1 < x\leq \sqrt{3} \\ 1 & x > \sqrt{3} \end{cases}$$

Now $U$: $$U = x^3$$ $$x = \sqrt[3]{U}$$
$$U = \frac{1}{2}x^2-\frac{1}{2}$$
$$x = \sqrt{2U+1}$$
Algorithm:
1. Generate $U_1\sim U(0,1), U_2\sim U(0,1)$
2. if $U_1 \leq \frac{1}{2}$ return $x = \sqrt[3]{U_2}$ else return $x = \sqrt{2U+1}$

TODO ADD Composition exercise 23 slides!!

---
#### Acceptance-Rejection

This method is less direct than previous methods. Can be useful when previous methods fail or are inefficient. 
Specify a function $t$, called the majorizing function, such that $t(x) \geq f(x)$ for all $x$.

- $t(x)$ majorizing function
- $r(x) = \frac{t(x)}{c}$ is pdf
- $c = \int_{-\infty}^\infty t(x)dx \geq \int_{-\infty}^\infty f(x)dx=1$

![[Screenshot 2023-11-28 at 12.22.59 PM.png|300]]

**Algorithm**
1. Generate $Y$ having density $r$
2. Generate $U\sim U(0,1)$ independent of $Y$
3. If $U\leq \frac{f(Y)}{t(Y)}$ return $X=Y$
4. Else go to 1

![[Screenshot 2023-11-28 at 12.25.53 PM.png|350]]

> More efficient choice:

![[Screenshot 2023-11-28 at 12.26.46 PM.png|350]]

---
**Example**

$$f(x) = \begin{cases} 30x^5 - 60x^4 +32x^3 & 0\leq x\leq 1 \\ 0 & else \end{cases}$$
TODO SOLVE!

----
#### Convolution

For several important distributions, the desired random variable $X$ can be expressed as the sum of other IID random variables.
The other random variables ($Y$) can be generated more readily than $X$. $$X = Y_1+Y_2+Y_3+...+Y_m$$
**Algorithm**
1. Generate $Y_1,Y_2,...,Y_m$ IID each with distribution function $G$
2. Return $X = Y_1+Y_2+...+Y_m$

> Bad way of generating Gaussian variates!:

Let $U_1,U_2,..,U_{12}\sim U(0,1)$
Then $X=U_1+U_2+...+U_{12}-6$ is approximately normally distributed
Relies on central limit theorem! No tails!
Uses a lot of random numbers.

----
#### Generating continuous random variates

> Uniform distribution

Distribution function of a $U(a,b)$ random variable is inverted by solving $U=f(x)$ for $x$.

For $0\leq u\leq 1$ $$x= F^{-1}(u)=a+(b-a)u$$
Use the inverse-transform method to generate $X$:
1. Generate $U\sim U(0,1)$
2. Return $X= a+(b-a)U$

> Exponential

Use inverse-transform method.

> m-Erlang

Use convolution (sum of exponentials) or inverse-transform method.

>Lognormal

Use the following algorithm:
1. Generate $Y\sim N(\mu,\sigma^2)$
2. Return $X=e^Y$

>Normal

Box and Muller method (SEE CLIP!)
Polar method