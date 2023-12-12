
![[Screenshot 2023-11-13 at 11.23.53 AM.png|500]]

Test statistic: $$X^2 = \sum_{j=1}^k \frac{(N_j-np_j)^2}{np_j}$$
in which, $$n = \sum_{j=1}^kN_j$$
![[Screenshot 2023-11-13 at 11.26.51 AM.png|400]]

We are gonna compare the observations in intervals with number of observations we want to see. The probability of an observation landing in the particular interval.

Steps:
1. Divide the range of $\hat{F}$ into $𝑘$ adjacent intervals:  
		$[a_0,a_1),[a_1,a_2).[a_2,a_3),..., [a_{k-1},a_k)$
Per interval $[a_{j-1},a_j)$:  
1. Tally observations ($N_j$) in interval  
2. Compute expected proportion $p_j$ based on $\hat{F}$

![[Screenshot 2023-11-13 at 11.31.41 AM.png|400]]

If $\hat{F}$ is continuous: $$p_j = \int_{a_{j-1}}^{a_j}\hat{f}(x)dx$$
If $\hat{F}$ is discrete: $$\sum_{a_{j-a}\leq x_j\leq a_j} \hat{p}(x)$$
![[Screenshot 2023-11-13 at 11.35.57 AM.png|400]]

*Degrees of freedom*

* All parameters known:
	* $𝑘 − 1$ degrees of freedom
* $m$ parameters estimated from data:  
	* $𝑘 − 1 − 𝑚$ degrees of freedom

**Example**:
10,000 random numbers $X_i \sim U(0,1)$.  
Perform a $X^2$ test with $\alpha= 0.05$.
1000 observations expected for each bin ($np_j$) and number of actual observations ($N_j$).

$X^2 = \sum_{j=1}^k \frac{(N_j-np_j)^2}{np_j}$

$[0,0.1) \rightarrow \frac{(1013-1000)^2}{1000} = 0.169$

![[Screenshot 2023-11-13 at 11.43.33 AM.png]]

$X^2 = \sum_{j=1}^k \frac{(N_j-np_j)^2}{np_j} = 10.88$

Critical Value (9 degrees of freedom (k-1)): $c_{1-\alpha}= 16.92$ 
If $X^2 < c_{1-\alpha} \rightarrow$ no reason to reject
