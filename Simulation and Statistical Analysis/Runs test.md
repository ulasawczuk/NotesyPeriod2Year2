>Tests independence of random numbers: $$u_k \sim U(0,1)$$

Various runs tests exist!  

- Run: a sequence of consecutive observations  
	- <font color="#e36c09">above</font> the mean (denoted by 𝑎) or  
	- <font color="#4f81bd">below</font> the mean (denoted by 𝑏).

![[Screenshot 2023-11-18 at 4.04.37 PM.png|400]]

Under $H_0$, the total number of runs (denoted by $r$) becomes approx. normally distributed (if $a > 20$ or $b>20$) with $$\mu_r=\frac{2ab}{n}+0.5$$ $$\sigma^2_r=\frac{2ab(2ab-n)}{n^2(n-1)}$$
Test statistic:$$R =\frac{r-\mu_r}{\sqrt{\sigma^2_r}}$$
Region of acceptance:$$-z_{\frac{\alpha}{2}}\leq R\leq z_{\frac{\alpha}{2}}$$
#### Example

Given the following table with random numbers, where the first five numbers are in the first column, etc:
![[Screenshot 2023-11-18 at 4.11.25 PM.png]]

Perform a runs test ($\alpha = 0.05$) to determine whether you may reject the null hypothesis that these are random independent draws form the $U(0,1)$ distribution. What are your conclusions?

<font color="#e36c09">Above the mean</font>
<font color="#4f81bd">Below the mean:</font>
![[Screenshot 2023-11-18 at 4.13.25 PM 1.png]]

* a = 25
* b = 25
* r = 25
* $\mu_r = \frac{2ab}{n}+\frac{1}{2}=25.5$
* $\sigma^2_r=\frac{2ab(2ab-n)}{n^2(n-1)} = 12.2449$
* $R= \frac{e-\mu_r}{\sqrt{\sigma^2_r}} = \frac{7\sqrt{6}}{120}\approx - 0.1429$
* $\alpha=0.05 \rightarrow z_{\frac{\alpha}{2}}=1.96$
- $-z_{\frac{\alpha}{2}} \leq R \leq z_{\frac{\alpha}{2}} \rightarrow -1.96 \leq -0.1429 \leq 1.96$, so no reason to reject $H_0$!

