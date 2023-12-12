>Tests independence of random numbers: $$u_k \sim U(0,1)$$

Steps:
1. construct $$y_k = \floor{10*u_k}$$
2. group per 5 observations $$y_{5j},y_{5j+1}y_{5j+2},y_{5j+3},y_{5j+4}$$
3. count occurrences of patterns in the table

![[Screenshot 2023-11-17 at 12.56.04 PM.png|500]]

We know that patterns happen with certain probability. We can do Chi squere test as we have probabilities and bins.