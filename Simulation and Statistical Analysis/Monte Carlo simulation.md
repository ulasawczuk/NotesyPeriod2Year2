A Monte Carlo simulation is a mathematical technique that simulates the range of possible outcomes for an uncertain event. 
It employs random numbers to solve problems.
The techniques are stochastic. (if you ever hear “stochastic simulation” it just means there is randomness involved)
Typically, one runs simulations many times over in order to obtain the distribution of an unknown probabilistic entity.

**Example:** Buffon's needle

![[Screenshot 2023-11-01 at 1.40.17 PM.png|500]]
Let $l$ be the length of the line, $A$ the distance from the line to the border line and $\theta$ the acute angle between the needle and the line. We have a line crossing (needle crosses the line) if $A$ is smaller than $l * sin(\theta)$. The position of the needle is anywhere between the two lines. We also have a theta $\theta$ the angle, which is an element from \[0, 2$\pi$\] this is because the needle is symmetric and we cannot distinguish the bottom from the top. We say that every $A$ is equally likely and every $\theta$ also. Therefore, the PDF becomes $\frac{1}{\delta} * \frac{1}{\pi}$ . The reason we can multiply these two factors is because we assume independence on these variables. Now we can find the expected value. We define the situation a line crossing equating to one, while no line crossing equates to zero. Because we are working continuously, we do not have a sum of probabilities but rather than an integral. We define the integral: $$\int_0^\pi \int_A^{l * sin(\theta)} 1 * \frac{1}{\delta\pi} dAd\theta$$
Because the term $\frac{1}{\delta\pi}$ has no $A$ terms we can treat it as a constant for the inner integral. We rewrite the integral: $$\int_0^\pi \frac{1}{\delta\pi} \int_A^{l * sin(\theta)} 1 dAd\theta$$
We compute the inner integral and integrate with respect to $A$. The integral becomes: $$\int_0^\pi l* \frac{sin(\theta)}{A\pi}d\theta$$
Now let's compute this integral. The inside becomes: $$-l * \frac{cos(\theta)}{\delta\pi}$$
Let's evaluate it from $0$ to $\pi$: $$-l * \frac{cos(\pi)}{\delta\pi} -l * \frac{cos(\theta)}{\delta\pi}$$
Which equals to: $$\frac{l}{\delta\pi} + \frac{l}{\delta\pi} = \frac{2l}{\delta\pi}$$
This is our probability of needle crossing.
If the needle is dropped $n$ times the expected number of crossings is equal to $\frac{2nl}{\delta\pi}$.  

#### Monte Carlo integration
---
* Suppose we want to evaluate the integral $I = \int_a^b g(x)dx$, where $g(x)$ is real-valued and possibly not analytically integrable.
* Let $Y$ be the random variable $Y = (b-a)g(X)$, where $X - U(a,b)$.
* Then $I = E(Y)$.
* Where we use $$\bar{Y} = (b-a)\frac{\sum_{i=1}^{n}g(X_i)}{n}$$
as unbiased estimator. The sampling mean approximates $E(Y)$.

**Proof**
$$Y = (b-a)g(x)$$
$$E(Y) = E((b-a)g(X))$$
$$E(Y) = (b-a)E(g(X))$$$$E(Y) = (b-a)\int_a^bg(x)f_x(x)dx$$ (LOTUS :00)
$$E(Y) =(b-a)\int_a^b\frac{g(x)}{b-a}dx$$

$$E(Y) = \int_a^bg(x) = I$$


#### Higher order integration (Lab 1)
---

Consider the following integral: $$\int_0^\frac{5}{4}\int_1^\frac{7}{2}4-x^2-y^2dydx$$
We want to approximate it using Monte Carlo method.
Let $$X \sim U(0,\frac{5}{4})$$and $$Y \sim U(1,\frac{7}{2})$$
We want to find $S = I$
$$S =(\frac{5}{4}-0)(\frac{7}{2}-1)[4 - X^2 - Y^2]$$
Here we replaced $x,y$ with random variables $X,Y$.
Now let's find $\bar{S}$. $$\bar{S} = \frac{25}{8}\frac{\sum_{i=1}^n(4-X_i^2-Y_i^2)}{n}$$
Calculate in matlab:
```matlab
% function (g(x))
func = @(x,y) (4 - x.^2 - y.^2);

% Num of simulations
n = 100000;

% Uniform distributions of r.v.s X,Y
xVal = rand(n, 1) * 5/4;
yVal = rand(n, 1) * 2.5 + 1;

% summing up the outcomes of function
sum = 0;
for i = 1:n
	sum = sum + func(xVal(i),yVal(i));
end

% monte carlo method to approximate the integral
monteCarlo = @(n) (25./8).*(sum./n);
monteCarlo(n)
```
Answer: $\sim\sim$ -6.5962

Now check with *integral* function in matlab:
```matlab
integral2(func,1,7/2,0,5/4)
```
Answer: $\sim\sim$ -6.5755

