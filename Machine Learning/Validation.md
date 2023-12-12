
It is important to validate classifier’s generalization performance in order to:
- Determine whether to employ the classifier; 
	<u>For example</u>: when learning the effectiveness of medical treatments from a limited-size data, it is important to estimate the accuracy of the classifiers.
- Optimize the classifier. 
	<u>For example</u>: when post-pruning decision trees we must evaluate the accuracy of the decision trees on each pruning step.

**Fundamental Problem in Predicition**

- When making predictions, a model usually makes some error.  
- The prediction error can be decomposed into a bias, a variance and a residual term.  
- Models tend to trade off error bias and variance.  
- As data scientists, we try to minimize both.

**Error Bias-Variance Tradeoff**

![[Screenshot 2023-11-15 at 3.45.29 PM.png|400]]

----
#### Confusion Matrix

A **confusion matrix** is a summary of prediction results on a classification problem. It lists correctly and falsely classified instances by class. E.g. in a problem with two classes $Y =$ {$+,-$} it lists true positives ($TP$), false positives ($FP$), true negatives ($TN$) and false negatives ($FN$). 

![[Screenshot 2023-11-16 at 12.35.45 PM.png|300]]

---
#### Evaluation Metrics

![[Screenshot 2023-11-15 at 3.51.20 PM.png|400]]

Take an image classifier that outputs whether an image contains a human face.
The classifier's performance on a <u>test set</u> is depicted in the above confusion matrix.
Here we have a binary classification.

- Accuracy: Ratio of correctly classified instances$$\frac{TP+TN}{P+N} = \frac{40+30}{50+50} = 0.70$$
- Error: Ratio of incorrectly classified instances $$\frac{FP+FN}{P+N} = \frac{20+10}{50+50} = 0.30$$
- Precision: Ratio of true positives in all as + classified instances $$\frac{TP}{TP+FP} = \frac{40}{40+20} = 0.67$$
- TP Rate: (Sensitivity) Ratio of true positives in all positive instances $$\frac{TP}{P} = \frac{40}{50}= 0.80$$
- FP Rate: Ratio of false negatives in all negative instances$$\frac{FP}{N}=\frac{20}{50} =0.40$$

![[Screenshot 2023-11-15 at 4.23.45 PM.png|500]]

---
#### Cost-Sensitive Metrics

In practice, different types of classification errors often incur different costs.
TP and TN cost is often 0.
Examples:
- Promotional mailing
- Terrorist profiling
- Loan decisions
- Fault diagnosis

![[Screenshot 2023-11-15 at 4.28.01 PM.png|300]]

##### Classification

If the classifier provides a probability for each class, the output can be adjusted to minimize the expected costs of the predictions.
**Expected cost** is computed as dot product of vector class probabilities and appropriate column in cost matrix.


- Cost **Yes** = $0.6*0+0.4*10=4$ | ![[Screenshot 2023-11-15 at 4.32.23 PM.png|200]]
- Cost **No** = $0.6*5+0.4*0=3$ 

##### Cost Sensitive learning

-> Simple methods for cost sensitive learning:
- Resampling of instances according to costs before training
- Weighting of instances according to costs during training.
	 
-> When using a toolbox:
- In Weka, Cost Sensitive Classification and Learning can be applied for any classifier using the meta scheme CostSensitiveClassifier.
- In SciKit-Learn many metrics offer weighting as a parameter

---
#### Estimations

**On which Data shall the metrics be estimated?**

* [[Estimation with training data]]
* [[Estimation with Independent Set Data]]
* [[Hold-out method]]
* [[k-fold Cross-Validation method]]
* [[Leave-one-out method]]
* Bootstrap method
	* Randomly draw dataset from the training sample
	* Each bootstrap sample is the same size as the training sample
	* Refit the model with the bootstrap sample
	* Repeat
	* Validate on actual training sample

* Large data:
	* Use test sets and hold-out method,
	* splitting is not expensive and doing cross-validation would be costly
- Middle-sized data:
	- Use cross-validation its perfect for it
- Small data:
	- Use leave-one-out,
	- can only be used efficiently on small data either way
* Don't use test data for parameter tuning - use separate validation data

---
#### Confidence intervals for Errors

> A classifier’s $error_S(h)$ is estimated on test data.

How close is the estimated $error_S(h)$ to the true $error_D(h)$?

![[Screenshot 2023-11-15 at 5.26.43 PM.png|300]]

$$CI = e_s(h) \textpm Z_n \sqrt{\frac{e_S(h)(1-e_S(h))}{n}}$$

**If** the *test data* contains at least 30 independent instances
**Then** the true but unknown $error_D(h) = 𝑒_𝐷$ lays in the interval around the estimated $error_S(h) = 𝑒_𝑆$ with a confidence of N%.

N% | 50 | 68 | 80 | 90 | 95 | 98 | 99
--|--|--|--|--|--|--|--
$Z_N$ | 0.67 | 1.00| 1.28 | 1.64 | 1.96 | 2.33 | 2.58

---
#### Ranking Classifiers

- Some classifiers output only a label
- Other classifiers indicate how certain they are that a given instance belongs to a class
- These scores (often probabilities) allow to rank instances according to their class resemblance

![[Screenshot 2023-11-15 at 5.41.10 PM.png|500]]

- Predicted class scores allow to choose a decision threshold: Output Yes **if** Score(yes) $\geq t$.
- Each threshold $t$ results in a new version of the classifier.  
- **High threshold** -> mostly No outputs (conservative)  
- **Low threshold**-> mostly Yes outputs (liberal)
---
#### [[Receiver Operating Characteristic]]

