
> The performance of a ranking classifier depends on the chosen **threshold**.

How should the threshold be chosen?
Calculating all of the different sensible thresholds and their confusion matrices would result in an unimaginable amount of said matrices. Instead of looking at them, use **Receiver Operatior Characteristic (ROC) Curve**.

![[Screenshot 2023-11-15 at 5.45.35 PM.png|500]]

---
#### ROC Space

An ROC graph summarizes all of the confusion matrices that each thershold produces.
- graph $TPr$ (sensitivity) on $y-axis$
- graph $FPr$ (1-specificity) on $x-axis$
- diagonal 45 degrees line through the origin shows where $TPr = FPr$ (matches random performance)

![[Screenshot 2023-11-15 at 5.47.08 PM.png|400]]

---
#### Dominance

> Classifier A dominates classifier B if and only if $TPr_A > TPr_B$ and $FPr_A < FPr_B$.

---
#### How to construct ROC Curve for Ranking (Probabilistic) Classifier Efficiency?

1. Sort the test instances into list $T$ decreasing order of the probability $P_{pos}$ of being positive computed by scoring classifier $h$.
2. **For** each consecutive instance $x$ in list $T$ **do**:
	1. Set threshold value $t$ equal to the probability $P_{pos}$ of $x$ and compute TPr and FPr of the discrete classifier $h_t$.
	2. Plot the TPr and FPr rates of the discrete classifier $h_t$.

![[Screenshot 2023-11-15 at 5.59.13 PM.png|200]]

We start with instance with probability 0.99.

![[Screenshot 2023-11-15 at 6.01.10 PM.png|400]]

Calculations:
$TPr =\frac{TP}{P}= \frac{0}{3}=0$
$FPr = \frac{FP}{N}=\frac{0}{2}=0$
So we get point (0,0)

Move on to instance with probability 0.98, update the confusion matrix by moving one instatnce to its true class (in this case we move one from FN to TP) and calculate next point.

![[Screenshot 2023-11-16 at 1.06.42 PM.png|400]]

Calculations: 
$TPr = \frac{TP}{P} = \frac{1}{3}$
$FPr = \frac{FP}{N} = \frac{0}{2}= 0$
We get next point (0,$\frac{1}{3}$)

Continue until the last instance (0.43, neg) we have this confusion matrix, we calculate last point and plot it.

![[Screenshot 2023-11-16 at 1.12.47 PM.png|400]]

Calculations:
$TPr = \frac{3}{3}=1$
$FPr = \frac{2}{2} =1$
We get to last point (1,1)!

---
#### ROC for one Classifier

1. Good separation between the classes, convex curve.

![[Screenshot 2023-11-16 at 1.30.56 PM.png|200]]

2. Reasonable separation between the classes, mostly convex.

![[Screenshot 2023-11-16 at 1.16.23 PM.png|200]]

3. Fairly poor separation between the classes, mostly convex.

![[Screenshot 2023-11-16 at 1.17.30 PM.png|200]]

4. Poor separation between the classes, large and small concavities.

![[Screenshot 2023-11-16 at 1.29.43 PM.png|200]]

5. Random performance.

![[Screenshot 2023-11-16 at 1.31.27 PM.png|200]]

---
#### Area Under Curve (AUC)

The area under ROC curve (AUC) assesses the ranking in terms of separation classes. 
AUC estimates that a randomly chosen positive instance will be ranked before a randomly chosen negative instance.
Greater area -> better!

---
#### ROC Convex Hull (ROCCH)

> ROCCH is determined by the dominant classifiers, lying on the same iso-accuracy line.

- Classifiers on ROCCH achieve the best accuracy.
- Classifiers below ROCCH are always sub-optimal.
- Any performance on a line segment connecting two ROC points can be achieved by randomly choosing between them.
- The classifiers on ROCCH can be combined to form a hybrid.
- $FPr$ is often replaced with precision to handle negatively skewed sets.

---
#### ROC Curves and Analysis (3 Classifiers)

<font color="#00b050">Classifier 1</font>

|True/Predicted | pos     |  neg    |
|:-----|:-----|:-----|
|  pos    |  40    |  60    |
|   neg   |   30   |  70    |

$TPr = 0.4$
$FPr = 0.3$

<font color="#0070c0">Classifier 2</font>

|True/Predicted | pos     |  neg    |
|:-----|:-----|:-----|
|  pos    |  80    |  20    |
|   neg   |   50   |  50    |

$TPr = 0.8$
$FPr = 0.5$

<font color="#ff0000">Classifier 3</font>

|True/Predicted | pos     |  neg    |
|:-----|:-----|:-----|
|  pos    |  60    |  40    |
|   neg   |   20   |  80    |

$TPr = 0.6$
$FPr = 0.2$

##### Space & Dominance & ROCCH

![[Screenshot 2023-11-16 at 1.49.44 PM.png|500]]

Here red dominates green but not blue.

ROCCH:
![[Screenshot 2023-11-16 at 1.51.14 PM.png|500]]

---
#### Iso-Accuracy Lines

**Iso-Accuracy** line connects ROC points with the same accuracy $A$: $$A =\frac{P TPr + NTNr}{P+N}$$
Thus, the line has the function: $$TPr = \frac{N}{P}FPr+ \frac{A(P+N)-N}{P}$$
* Iso-Accuracy lines have slope $\frac{N}{P}$
* Higher iso-accuracy lines are better.

![[Screenshot 2023-11-16 at 2.02.53 PM.png|250]]

**Consider different iso-accuracy lines**

![[Screenshot 2023-11-16 at 2.04.48 PM.png|200]]

For a balanced class distribution, the iso-accuracy line has slope $\frac{N}{P}=1$.
$C4.5$ has an optimal accuracy of 82% among all classifiers shown.

![[Screenshot 2023-11-16 at 2.09.54 PM.png|200]]

With 4 times as many positives as negatives instances, the iso-accuracy line has slope $\frac{N}{P} = \frac{1}{4}$.
$SVM$ has an optimal accuracy of 84% among all classifiers shown.

![[Screenshot 2023-11-16 at 2.10.10 PM.png|200]]

With 4 times as many negative as positive instances, the iso-accuracy line has slope $\frac{N}{P} = 4$.
$CN2$ has an optimal accuracy of 86% among all classifiers shown.

![[Screenshot 2023-11-16 at 2.12.16 PM.png|200]]

With less than 9% positives, Always Negative is optimal.
With less than 11% negatives, Always Positive is optimal.
