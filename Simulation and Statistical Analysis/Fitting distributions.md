
>Why do we have fitting distributions?

* Simulation using random inputs  
	* Must specify probability distributions 
* Failure to choose a “correct” distribution can dramatically affect simulation results  
* In data analysis one often has to check whether the data indeed follows a certain distribution

----
#### Empirical Tests of Hypothesis

* Data: $X$
* Null-hypothesis: $H_0$
* Test statistic: $T$
* Significance level: $\alpha$
* Critical Value: $c$

![[Screenshot 2023-11-13 at 11.06.28 AM.png|550]]

We say that the null hypothesis is that a r.v. follows a particular function/distribution and an alternative to that is that it does not follow the function, if one holds the other one cannot:
$H_0: X \sim \hat{F}(x)$
$H_a: X ≁ \hat{F}(x)$

>Important!: If we refuse the null hypothesis (say that it does not follow given distribution) we still do not know what is the correct distribution of the variable

Test statistic quantifies how far off we are (can be calculated from data and null-hypothesis), $\alpha$ gives us the probability that we are wrong, it is our margin of error. The critical value is the point of the distribution of the test statistic where we get to $\alpha$.

![[Screenshot 2023-11-13 at 11.09.14 AM.png|200]]

----
#### Goodness of Fit Tests

**There is no perfect model**

Which distribution does the data follow?

![[Screenshot 2023-11-13 at 11.14.39 AM.png|500]]
Uniform :DDDD

Which distribution does the data follow?

![[Screenshot 2023-11-13 at 11.17.27 AM.png|500]]
WE have $\mu = 0$ and $\sigma = 1$ so it's Standard normal distribution.

Which distribution does the data follow?

![[Screenshot 2023-11-13 at 11.18.07 AM.png|500]]
Gamma distribution.

---
#### Statistical Tests

>Chi square test : $X^2$-test
>Kolmogorov-Smirnov test: KS test

[[Chi square test]]
[[Kolmogorov-Smirnov test]]

----
#### Selecting input distributions

---
#### Source of randomness

| Type of system |Sources of randomness  |
|:-----|:-----|
|  Manufacturing    | Processing times, machine times to failue     |
| Defense-related     | Arrival time and payloads of missiles  or airplanes, outcome of an engagement     |
|  Communications    |  Interarrival times of messages, message types, message lengths    |
|  Transportation    |  Ship-loading times, interarrival times of customer to a subway    |

##### Processes for selecting distributions

- Use data values themselves directly in the simulation  
- Define an empirical distribution function from the data values  
- Fit a theoretical distribution to the data  
- Obviously for random number generators the distribution is known to be U(0,1)

---
#### Skewness

Skewness is the extent to which the data are not symmetrical.
$$skew(X) = E[(\frac{X-\mu}{\sigma})^3]$$
![[Screenshot 2023-11-16 at 3.07.20 PM.png|300]]

---
#### Kurtosis

> Kurtosis indicates how the peaked distribution is.
> $Y'_2$ indicates how the peak and tails of a distribution differ from the normal distribution.

Use kurtosis to help you initially understand general characteristics about the distribution of your data.$$Kurt[X] = E[\frac{X-\mu^4}{\sigma}]$$
$$Y_2 = Kurt[X]-3$$
![[Screenshot 2023-11-16 at 3.13.10 PM.png|200]]

---
#### Activity 1: Hypothesizing Families of Distributions

>Process of determining appropriate general families of distributions, based on their shape.

-> Histogram
- Graphical estimate of plot of density function of the distribution  
- Constructed by breaking up values into adjacent intervals of the same width

-> Quantile summary
- Useful for determining whether the distribution is symmetric or skewed right or left  
- Box plot: its graphical representation

**How close to normal PDF?**

![[Screenshot 2023-11-16 at 3.22.07 PM.png|450]]

---
#### Activity 2: Estimating Parameters

> **Estimator**: 
> - Numerical function of the data  
> - Maximum-likelihood estimators (MLEs) considered here, but others like least squares also possible

![[Screenshot 2023-11-16 at 3.24.35 PM.png|500]]

- Given observations $X_1,X_2,...,X_n$
- The probability of seeing $X$, given $\mu$ and $\sigma$ is $$P(X;\mu,\sigma) = \frac{1}{\sigma\sqrt{2\pi}}e^{\frac{-(X-\mu)^2}{2\sigma^2}}$$
- The joint probability fro these observations assuming independence is: $$P(X_1,X_2,...,X_n;\mu,\sigma) = \Pi_{i=1}^n \frac{1}{\sigma\sqrt{2\pi}}e^{\frac{-(X-\mu)^2}{2\sigma^2}}$$
MAXIMIZE!
- The log-likelyhood is $$ln(P(X_1,X_2,...,X_n;\mu,\sigma)) = \sum_{i=1}^n [ln(\frac{1}{\sigma\sqrt{2\pi}})\frac{-(x_i-\mu)^2}{2\sigma^2}]$$
- You find the desired estimater by finding where the derivative is 0, e.g. $$\frac{d}{d\mu}ln(P(X_1,X_2,...,X_n;\mu,\sigma)) = 0$$


