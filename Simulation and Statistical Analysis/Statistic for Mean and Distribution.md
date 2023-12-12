#### Hypothesis Testing

[[Hypothesis testing]]

---
#### Hypothesis tests for the mean

Data: $X$
Null-hypothesis: $H_0$
Alternative hypothesis: $H_a$
Test statistic: $T$
Significance level: $\alpha$
$$H_0 = \mu_X = \mu_0$$

| One-sided     |  Two-sided    |  One-sided    |
|:-----|:-----|:-----|
|   $H_0:\mu_X=\mu_0$   |  $H_0:\mu_X=\mu_0$    |   $H_0:\mu_X=\mu_0$   |
|   $H_a: \mu_X<\mu_0$   |  $H_0:\mu_X\neq \mu_0$    |    $H_0:\mu_X>\mu_0$  |
![[Screenshot 2023-11-27 at 11.45.19 AM.png|300]]

>**$p$-value**
>The probability, assuming $H_0$ is true, that the test statistic would take a value as extreme or more extreme than that actually observed is called the $𝒑$-value of the test. The smaller the $𝑝$-value, the stronger the evidence against $𝐻_0$ provided by the data.

Suppose test statistic $T=t$, than the $p$-value for a test of $H_0:\mu_X=\mu_0$ against 

|$H_0:\mu_X>\mu_0$    |  $H_0:\mu_X<\mu_0$   |  $H_0:\mu_X=\mu_0$  |
|:-----|:-----|:-----|
|  is $P(T \geq t)$   |  is $P(T \leq t)$     |is $2*P(T\geq \left\lvert t \right\rvert)$ |
![[Screenshot 2023-11-27 at 11.53.21 AM.png|300]]

> **Statistical significance**
> If the $𝑝$-value is as small or smaller than $\alpha$, we say that the data are statistically significant at level $\alpha$.

> **Power**
> The probability that a level $\alpha$ significance test will reject $H_0$ when a particular alternative value of the parameter is true is called the **power** of the test to detect that alternative.

----

![[Screenshot 2023-11-27 at 11.59.20 AM.png|500]]

**Significance and Type I Error**
The significance level $\alpha$ of any fixed level test is the probability of Type I Error.
**Power and Type II Error**
The power of a fixed level test to detect a particular alternative is 1 minus the probability of a Type II Error for that alternative.

----
#### Examples of hypothesis tests for the mean

* [[z-test for the Mean]]
* [[t-test for the Mean]]

---
#### Comparing two means

Suppose we have two data sets $X_1$ and $X_2$. There are the following situations that we can consider.

![[Screenshot 2023-11-27 at 12.33.48 PM.png|450]]

---
#### Matched pairs t-test

- In each experiment, two observations are paired  
- Outcomes are compared within pairs  
- Look at differences rather than absolute values 
- Common when randomization is not possible  
- Examples:  
	- Same subjects under different conditions  
	- Before and after some intervention

Suppose $\bar{\delta}(n)=\bar{X}(n)-\bar{X}_2(n)$ is normally distributed, $\sigma^2$ is unknown. We test $H_0: \mu_{X_1}-\mu_{X_2}= \delta_0$ against $H_a: \mu_{X_1}-\mu_{X_2}\neq  \delta_0$ at significance level $\alpha$.
Test statistic: $$t_n=\frac{\bar{\delta_X}-\delta_0}{\sqrt{\frac{S^2_{\delta}(n)}{n}}}$$
Reject $H_0$ if |$t_n$| $>t_{n-1,1-\frac{\alpha}{2}}$

![[Screenshot 2023-11-27 at 12.40.38 PM.png|300]]

##### Example

![[Screenshot 2023-11-27 at 12.41.16 PM.png|450]]

---
#### Independent samples (Welch's) t-test

Suppose $\bar{X}_1(n_1)$ and $\bar{X}_2(n_2)$ are normally distributed and $\sigma_{X_1}^2 \neq \sigma_{X_2}^2$ that are both unknown. We test $H_0: \mu_{X_1} = \mu_{X_2}$ against $H_a: \mu_{x_1} \neq \mu_{X_2}$ at significance level $\alpha$. 
Test statistic: $$t= \frac{\bar{X}_1(n_1))-\bar{X}_2(n_2)}{\sqrt{\frac{S_1^1(n_1)}{n_1}+\frac{S_2^2(n_2)}{n_2}}}$$
Reject $H_0$ if |$t$| $> t_{\hat{f},1-\frac{\alpha}{2}}$

![[Screenshot 2023-11-27 at 12.47.38 PM.png|300]]

----
#### Pooled t-test

Suppose $\bar{X}_1(n_1)$ and $\bar{X}_2(n_2)$ are normally distributed and $\sigma_{X_1}^2 \neq \sigma_{X_2}^2$ that are both unknown. We test $H_0: \mu_{X_1} = \mu_{X_2}$ against $H_a: \mu_{x_1} \neq \mu_{X_2}$ at significance level $\alpha$. 
Test statistic: $$t= \frac{\bar{X}_1(n_1)-\bar{X}_2(n_2)}{\sqrt{S_p^2(\frac{1}{n_1}+\frac{1}{n_2})}}$$
with $n_1+n_2-2$ degrees of freedom.
and $S_p^2=\frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}$
Reject $H_0$ if |$t$|$> t_{n_1+n_2-2, 1-\frac{\alpha}{2}}$

![[Screenshot 2023-11-27 at 12.52.40 PM.png|300]]

----
#### Departures from normality

> Dealing with non-normality

All test covered thus far assume normality of observations or differences. But what can we do if this is not true?  
1. Remove outliers  
2. Transform data (e.g., by log-scaling)  
3. Use other standard distributions (e.g., exponential)  
4. Use Bootstrap methods (discussed in Lecture 10)  
5. Use non-parametric tests
---
#### Nonparametric tests

**Hypothesis Tests using Ranks**

Data: $X$
Null-hypothesis: $H_0$
Alternative hypothesis: $H_a$
Test statistic: $T$
Significance level: $\alpha$
$$H_0: P(X_1>X_2) = \frac{1}{2}$$

| One-sided     |  Two-sided    |  One-sided    |
|:-----|:-----|:-----|
|   $H_0:P(X_1>X_2) = \frac{1}{2}$  | $H_0:P(X_1>X_2) = \frac{1}{2}$  |  $H_0:P(X_1>X_2) = \frac{1}{2}$|
|   $H_a:P(X_1>X_2) < \frac{1}{2}$|$H_a:P(X_1>X_2) \neq \frac{1}{2}$ |  $H_a:P(X_1>X_2) > \frac{1}{2}$  |
![[Screenshot 2023-11-27 at 12.59.25 PM.png|450]]

Instead of actual values, these nonparametric tests use ranks of observations. 


|  Setting    | Normal test     |  Rank test    |
|:-----|:-----|:-----|
|  One sample    |   One-sample $t$-test   |  Wilcoxon signed rank test    |
|  Matched pairs    |  Apply one-sample test to difference in samples   |      |
|   Two independent samples   |  Two-sample $t$-test    | Wilcoxon rank sum test     |

**Computing ranks**
- Order all observations in ascending order.  
- Assign ranks to all observations, starting with 1 and ending with $n$.  
- Deal with ties: all observations get the average rank of tied observations.

----
#### Example

A study of early childhood education asked kindergarten students to retell two fairy tales that had been read to them earlier in the week. The 10 children in the study included five high-progress readers and five low-progress readers. Each child told two stories. Story 1 had been read to them; Story 2 had been read and also illustrated with pictures. An expert listened to a recording of each child and assigned a score for certain uses of language.

![[Screenshot 2023-11-27 at 2.20.57 PM.png|200]]

---
#### Wilcoxon signed Rank test

We test $H_0: P(X_1 > X_2)=\frac{1}{2}$ against $H_a: P(X_1>X_2)\neq \frac{1}{2}$.
Test statistic: $W^+$ equals the sum of ranks in sample $X_1$ and $$\mu_{W^+}= \frac{n(n+1)}{4}$$ $$\sigma_{W^+}= \sqrt{\frac{n(n+1)(2n+1)}{24}}$$
**Normal approximation of $W^+$**
$z = \frac{W^+-\mu_{W^+}}{\sigma_{W^+}}$
Reject $H_0$ if |$z_n$| $> z_{1-\frac{\alpha}{2}}$

![[Screenshot 2023-11-27 at 2.27.48 PM.png|300]]

However we have to apply **Continuity correction**!

**Continuity correction**
Ranks are integer valued, but the normal distribution is continuous.

![[Screenshot 2023-11-27 at 2.29.18 PM.png|450]]

---
#### Example

$H_0$: Scores have the same distribution for both stories.
$H_a$: Scores are systematically higher for Story 2.

![[Screenshot 2023-11-27 at 2.30.14 PM.png|200]]

----
#### Wilcoxon rank sum test

We test $H_0: P(X_1 > X_2)=\frac{1}{2}$ against $H_a: P(X_1>X_2)\neq \frac{1}{2}$.
Test statistic: $W^*$ equals the sum of ranks in sample $X_1$ and $$\mu_{W^*} = \frac{n_1(n_1+n_2+1)}{2}$$ $$\sigma_{W^*}= \sqrt{\frac{n_1n_2(n_1+n_2+1)}{12}}$$
**Normal approximation of $W^*$**
$z = \frac{W^*-\mu_{W^*}}{\sigma_{W^*}}$
Reject $H_0$ if |$z_n$| $> z_{1-\frac{\alpha}{2}}$

Again, we do have to apply a continuity correction!

----
#### Example

$H_0$: Scores have the same distribution for both progress levels.
$H_a$: Scores are systematically higher for high-progress students.

![[Screenshot 2023-11-27 at 2.35.14 PM.png|200]]


