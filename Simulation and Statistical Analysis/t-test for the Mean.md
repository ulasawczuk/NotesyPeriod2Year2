$\bar{X}(n)$ is normally distributed, $\sigma^2$ is unknown:
Estimate variance from data: $$S^2(n)=\frac{\sum_{i=1}^n(X_i -\bar{X}(n))^2}{n-1}$$
However this adds uncertainty. 
**Solution:** Student $t$ with $n-1$ dof instead of Normal.

![[Screenshot 2023-11-27 at 12.27.59 PM.png|300]]

We test $H_0: \mu_X = \mu_0$ against $H_a = \mu_X \neq \mu_0$ at significance level $\alpha$.
Test statistic: $$t_n=\frac{\bar{X}(n)-\mu_0}{\sqrt{\frac{S^2(n)}{n}}}$$
Reject $H_0$ if |$t_n$|$>t_{n-1,1-\frac{\alpha}{2}}$

![[Screenshot 2023-11-27 at 12.30.23 PM.png|300]]

---
#### Exercise

A test of the null hypothesis $H_0: \mu_X=40$ against the alternative hypothesis $X_a: \mu_X \neq 40$ from a sample of 13  
observations has the value $t$ = 2.78.  
1. Is the value $t$ = 2.78 statistically significant at the 5% level? At the 1% level?
