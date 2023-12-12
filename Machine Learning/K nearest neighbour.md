#### Classification problem 

**Given:**
* Set {$X_p$}$_{p\in{1,...P}}$ of P input variables that define the input space $X$
* Discrete output variable $Y$
* Unknown probability distribution $𝑄$ over $𝑋 × 𝑌$ ($Q$ stands for the phenomena under study
* Labeled training data $𝐷 ⊆ 𝑋 × 𝑌$ generated from $𝑄$
**Find:**
* Value $𝑦 ∈ 𝑌$ of a test instance $𝑥$ according to $𝑄$.

---
#### k-NN Classifier

What is the dimensionality of the in- and output space?
Input space: 2, output space: 1

![[Screenshot 2023-11-14 at 3.05.53 PM.png|300]]

If we look inside the space how many instances are similar?

---
#### Instance space and distances

Let us denote the value of p-th variable $𝑋_𝑝$ for instance $𝑥_𝑖$ by $𝑥_𝑖𝑝$. Then:
* If the p-th variable is numeric, then the distance $𝑑_𝑝$ between instances $𝑥_𝑖$ and $𝑥_𝑗$ for the p-th variable is equal to: $$d_p(x_i,x_j)= \frac{|x_{ip}-x_{jp}|}{rangeOfX_p}$$
* If the p-th variable is *discrete*, then the distance $𝑑_𝑝$ between instances $𝑥_𝑖$ and $𝑥_𝑗$ for of p-th variable is equal to: $$d_p(x_i,x_j) = 0$$ if $x_{ip} =x_{jp}$ $$d_p(x_i,x_j) = 1$$
 if $x_{ip} ≠ x_{jp}$ 

![[Screenshot 2023-11-14 at 3.11.20 PM.png|300]]

[[Minkowski Distance]]

> **Continuous variables should be normalized**. Otherwise, the variables with bigger domains prevail!
> **Discrete variables** do not pose problems since distances are based on value matches.

---
To estimate a class value $y$ for a given test instance $x$, find a set $NN$ of the **$k$ closest instances** to $x$ in  
training data $D$.

**Discrete classification:** output the majority class among the instances in $NN$.
**Scoring classification:** output the score for each class among the instances in $NN$. If the scores are normalized we estimate class probabilities.

1 vs 5 neighbours

![[Screenshot 2023-11-14 at 3.26.29 PM.png|300]]

1-nearest neighbour: test instance is classified positive
5-nearest neighbour: test instance is classified negative  

---
#### Classification & Decision boundaries

For 1-nn, one can construct decision boundaries by creating a bounding polyhedron around each training instance.
A test instance will be located in one such polyhedron and receive the corresponding class.
For $k>1$, the decision boundaries are more difficult to assess.

**Meaning of k**
The value of k controls the *complexity* and *locality* of the decision border of the k-NN classifier. The smaller that value the more complex is the decision border of the k-NN classifier since it becomes more local.

---
##### Exercise
Inspect the diagrams and indicate whether k is small, medium or large.

![[Screenshot 2023-11-14 at 3.30.03 PM.png|600]]

We can see that going from left to right diagram k will grow as in the first one the border is the most complex. Respectively to diagrams from left to right: $k = 1, k=10,k=100$

##### Complexity exercise

1. Can KNN capture advanced patterns in the data? If yes, for which k?
**Yes**, KNN’s non-linear decision boundaries allow to capture complex patterns. This holds especially for small k.

2. Can it overfit, if yes, for which k?
**Yes**, KNN can easily overfit, especially for small k.

---

#### The Curse of Dimensionality

In a p=1 dimensional space, draw a radius around a point such that it captures 10% of the volume.
When p=1, the relation between radius and fraction of volume is linear.

![[Screenshot 2023-11-14 at 3.35.57 PM.png|600]]

In a p=2 dimensional space, the radius needs to be larger in order to capture 10% of the volume.
The relation between radius and fraction of volume is no longer linear.

![[Screenshot 2023-11-14 at 3.36.44 PM.png|600]]

> The higher the dimensionality p, the larger the radius needs to be, to cover the same fraction of volume.

Why is this a problem for KNN?  
It corrupts the distance measures. 

---
#### k-NN Regression

>What is the difference between classification and regression?  
>Classification predicts a discrete output variable while regression predicts a continuous output variable

To predict *output value y* for a given test instance x, consider a set *NN* of the *k* closest instances to *x* in training data *Tr* and take the average of the output values. i.e. $$f(X) = \frac{1}{k}\sum_{(x_i,y_j)\in NN}y_i$$
The value of *k* controls the complexity of the regression curve of the k-NN regression. The smaller that value the more complex is the regression curve of the k-NN regression.

![[Screenshot 2023-11-14 at 3.41.52 PM.png|500]]

What is the dimensionality of the in- and output space?  
- Input and output spaces are both 1 dimensional here  

Which model fits the data better ?  
- The right model  

Is k larger for the left or the right model?  
- Left: K=1, Right: K=9

---
#### Advantages and disadvantages of the standard NN Classifier

**Advatages:**
The NN Classifier:
1. can estimate complex class borders locally and differently for each new test instance;  
2. provides good generalization performance on many domains;  
3. learns very quickly;  
4. is robust to noisy training data;  
5. is intuitive and easy to understand which facilitates implementation and modification.

**Disadvantages:**
The NN Classifier:
1. has large storage requirements because it has to store all the data  
2. is slow during instance classification because all the training instances have to be visited;  
3. is susceptible to the curse of dimensionality  
4. has a generalization performance that degrades with increase of  
	1. noise in the training data;  
	2. irrelevant variables

---
#### Condensing

Aim is to reduce the number of training instances.
For each class, retain a set $S$ of instances needed to define the decision boundary. This is reminiscent of a Support Vector Machine.

<u>The Set S is Decision Boundary Consistent</u> – if the instances in $S$ impose a decision boundary that is identical to the boundary of the entire training set $D$.
<u>The Set S is a Minimum Consistent Set </u> - if it is the smallest subset of the training data that correctly classifies all of the original training data.

![[Screenshot 2023-11-14 at 3.48.39 PM.png|500]]

**Steps:**
1. For each class, initialize the set $S$ with a single training instance  
2. Classify all remaining instances in the training data $D$ using the instances in $S$, and transfer an arbitrary incorrectly classified instance to $S$.  
3. Return to 2 until no transfers occurred or the subset is full.

**Example:**

![[Screenshot 2023-11-14 at 3.51.33 PM.png|300]] $\rightarrow$![[Screenshot 2023-11-14 at 3.51.47 PM.png|300]]

![[Screenshot 2023-11-14 at 3.51.58 PM.png|300]]$\rightarrow$![[Screenshot 2023-11-14 at 3.52.08 PM.png|300]]

![[Screenshot 2023-11-14 at 3.52.21 PM.png|300]] DONE!

---
#### Condensed NN Classifier

The CNN algorithm is sensitive to noise, because noisy instances will usually be misclassified by their neighbors, and thus will be retained. This causes two problems:
1. storage reduction is hindered, because noisy instances are retained, and because they are there, often non-noisy instances nearby will also need to be retained.
2. generalization accuracy is hurt because noisy instances are usually exceptions and thus do not represent the underlying function well.

**Selecting attribute values**
- Search in the space of possible weights
- Each set of weights for all the input variables test using cross-validating k-NN

---
#### Edited NN Classifier

The Edited Nearest Neighbor classifier was proposed to stabilize the accuracy of the NN classifier when there is increase of noise in the training data.  
The algorithm starts with the set S equal to the training data D, and then each instance in S is removed if it does not agree with the majority of its k nearest neighbors (with k=3, typically).  
The algorithm edits out noisy instances as well as close border cases, leaving smoother decision boundaries. It also retains all internal points; i.e., it does not reduce the space as much as most other reduction algorithms.

![[Screenshot 2023-11-14 at 4.21.22 PM.png|200]]

This negative training instance is removed since it does not fit it’s neighbors!
The average reduction of the algorithm varies between 20% to 40%.

---
##### Exercise
**Combining KNN with other models**

![[Screenshot 2023-11-14 at 4.23.40 PM.png|200]]
How can you combine Decision Rules and KNN to classify these points more efficiently?
Use KNN to match a test instance with a cluster and then use decision rules within each cluster.
This can reduce the amount of storage of the model, since less instances need to be stored for the KNN part.

**Combining Decision Trees and Classifiers**

![[Screenshot 2023-11-14 at 4.25.45 PM.png|400]]

Classify the instance using the NN algorithm applied on the training instances associated with the classification nodes (leaves).

----
#### Summary

* Nearest-Neighbor (NN) Classifier is a non-linear method for classification.  
* NN can be a discrete classifier and a scoring classifier depending how we handle the class statistics of the nearest neighbors.  
* NN can be used for regression  
* Various adjustments  
	* Condensed KNN (Using only most informative neighbors) 
	* Attribute Weighted KNN  
	* Edited KNN (removal of noisy instances) 
	* Combination with other models