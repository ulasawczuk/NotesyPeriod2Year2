Minkowski distance is a distance between two instances $𝑥_𝑖$ and $𝑥_𝑗$ w.r.t. all the P variables that define the instance space $X$:
$$d(x_i,x_j) = \sqrt{d_1(x_i,x_j)^m + d_2(x_i,x_j)^m + ... + d_p(x_i,x_j)^m}$$

where m is the order (the distance so defined is also called L-m norm)

**Properties**:
* $d(x_i,x_j) > 0$ if $i ≠j$, and $d(x_i,x_j) = 0$ (Positive definitieness)
* $d(x_i,x_j) =d(x_j,x_i)$ (Symmetry)
* $d(x_i,x_j) < d(x_i,x_k) + d(x_k,x_j)$ (Triangle Inequality)

>A distance that satisfies these properties is a metric.

$m = 1$: Manhattan (city block, $L_1$ norm) distance
$$d(x_i,x_j) = d_1(x_i,x_j)^1 + d_2(x_i,x_j)^1 + ... + d_p(x_i,x_j)^1$$

$m = 2$: ($L_2$ norm) Euclidean distance $$d(x_i,x_j) = \sqrt{d_1(x_i,x_j)^2 + d_2(x_i,x_j)^2 + ... + d_p(x_i,x_j)^2}$$


$m \rightarrow \infty$ “supremum” ($L_{max}$ norm, $L_{\infty}$ norm) distance.  
* This is the maximum difference between any component (variable) of the vectors
$$d(x_i,x_j) = \lim_{m \rightarrow \infty}(\sum_{p=1}^pd_p(x_i,x_j)^m)^{\frac{1}{m}}=\max_pd_p(x_i,x_j)$$

![[Screenshot 2023-11-14 at 3.21.49 PM.png]]