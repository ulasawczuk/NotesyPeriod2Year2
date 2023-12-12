
Goodness of fit test for continuous distributions based on observations $X_1,X_2,X_3,...,X_n$.

![[Screenshot 2023-11-13 at 11.53.40 AM.png|400]]

Test statistic: $$D_n = sup|F_n(x)-\hat{F}(x)|$$
$F_n(x)$ - empirical distribution
$\hat{F}(x)$ - hypothesized distribution

##### Empirical distribution

W.l.o.g. assume that $X_1 <X_2<X_3<...<X_n$.

![[Screenshot 2023-11-13 at 11.57.13 AM.png|110]]|![[Screenshot 2023-11-13 at 11.58.25 AM.png|510]]

*KS-test critical values*
Depending on situation the test statistic needs to be modified and the critical values differ.

![[Screenshot 2023-11-13 at 12.01.18 PM.png|500]]

In Tadikamalla table of empirical determined critical values for vanilla test statistic for Gamma.
E.g. for Gamma with all parameters unknown:

![[Screenshot 2023-11-13 at 12.33.16 PM.png|500]]

#### **Test**

$H_0: X \sim U(2,6) \rightarrow$ |![[Screenshot 2023-11-13 at 12.34.26 PM.png|300]]
$\alpha = 0.05$

![[Screenshot 2023-11-13 at 12.35.01 PM.png|450]]|![[Screenshot 2023-11-13 at 12.35.46 PM.png|100]]

Depending on situation the test statistic needs to be modified and the critical values differ.

![[Screenshot 2023-11-13 at 12.37.34 PM.png|600]]

Critical value: $c_{1-\alpha} = 1.358$
Adjusted test statistic: $(\sqrt{6}+0.12+\frac{0.11}{\sqrt{6}})D_6$

> $D^+ = \max_{1\leq i \leq n}(\frac{1}{n}-\hat{F}(X_i)$

![[Screenshot 2023-11-13 at 12.41.08 PM.png|400]]

> $D^+ = \frac{4}{6}-\hat{F}(X_4) \approx 0.3038$

![[Screenshot 2023-11-13 at 12.42.10 PM.png|400]]

> $D^- = \max_{1\leq i \leq n}(\hat{F}(X_i)-\frac{i-1}{n})$

![[Screenshot 2023-11-13 at 12.44.37 PM.png|400]]

> $D^- = \hat{F}(X_6) - \frac{5}{6} \approx 0.1129$

![[Screenshot 2023-11-13 at 12.45.40 PM.png|400]]

Adjusted test statistic: $(\sqrt{6}+0.12+\frac{0.11}{\sqrt{6}})D_6 = 2.6144 * 0.3038 \approx 0.7943 < c_{1-\alpha}$
Thus we cannot reject $H_0$.

---
#### Example

Given the following (sorted) observations:

|  $X_1$    |  $X_2$     |   $X_3$    |     $X_4$  |  $X_5$     |  $X_6$     | $X_7$      |  $X_8$     |  $X_9$     |  $X_10$     |
|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|
| 0.1498 | 0.2116 | 0.2915  | 0.4013  | 0.5275 | 0.9569  | 1.1901  | 1.5157 | 2.0754  |   4.3005 |

Perform a Kolmogorov-Smirnov test ($\alpha = 0.05$) to test whether this data comes from an exponential distributions with parameter $\lambda = 1$ ($X\sim Exp(\lambda =1)$). Provide intermediate steps like the computations of $D^+, D^-, D_{10}$. What are your conclusions?

1. Perform a Kolmogorov-Smirnov test:

Calculate $D^+_i$ with $\frac{i}{n} - \hat{F}(X_i)$ for each $X_i$.

|Obs:|  $X_1$    |  $X_2$     |   $X_3$    |     $X_4$  |  $X_5$     |  $X_6$     | $X_7$      |  $X_8$     |  $X_9$     |  $X_10$     |
|: ---|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|
|Val: | 0.1498 | 0.2116 | 0.2915  | 0.4013  | 0.5275 | 0.9569  | 1.1901  | 1.5157 | 2.0754  | 4.3005 |
|$\hat{F}(X_i)$| 0.1391 | 0.1907|0.2528|0.3305|0.4099|06159|0.6958|0.7803|0.8745|0.9864 |
|$\frac{i}{n}$|0.1|0.2|0.3|0.4|0.5|0.6|0.7|0.8|0.9|1.0
|$\frac{i}{n} - \hat{F}(X_i)$|-0.0391|0.0093|0.0472|0.0695|0.0901|-0.0159|0.0042|0.0197|0.0255|0.0136

![[Screenshot 2023-11-16 at 2.32.20 PM.png|400]]

Thus, $D^+= \max{D^+_i}=0.0901$

Now to calculate $D^-$ let's calculate $\hat{F}(X_i) - \frac{i-1}{n}$ for each $X_i$.

|Obs:|  $X_1$    |  $X_2$     |   $X_3$    |     $X_4$  |  $X_5$     |  $X_6$     | $X_7$      |  $X_8$     |  $X_9$     |  $X_10$     |
|: ---|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|
|Val: | 0.1498 | 0.2116 | 0.2915  | 0.4013  | 0.5275 | 0.9569  | 1.1901  | 1.5157 | 2.0754  | 4.3005 |
|$\hat{F}(X_i)$| 0.1391 | 0.1907|0.2528|0.3305|0.4099|06159|0.6958|0.7803|0.8745|0.9864 |
|$\frac{i}{n}$|0.1|0.2|0.3|0.4|0.5|0.6|0.7|0.8|0.9|1.0
|$\hat{F}(X_i) - \frac{i-1}{n}$|0.1391|0.0907|0.0528|0.0305|0.0099|0.1159|0.0958|0.0803|0.0745|0.0864

![[Screenshot 2023-11-16 at 2.39.58 PM.png|400]]

Thus, $D^-= \max{D^-_i}=0.1391$

$D_{10} = \max(D^+,D^-)= 0.1391$

**Critical Value Choice**

Depending on situation the test statistic needs to be modified and the critical values differ.

![[Screenshot 2023-11-16 at 2.48.13 PM.png]]

$$(\sqrt{10}+0.12+\frac{0.11}{\sqrt{10}})D_{10} \approx 3.3171*D_{10}= 3.3171* 0.1391 = 0.4614 < c_{1-\alpha}$$
So, no reason to reject $H_0$!
$c_{1-\alpha} = 1.358$

