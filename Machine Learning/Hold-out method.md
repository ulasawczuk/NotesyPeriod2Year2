
>The hold-out method splits the data into training set and test set (66% for training, 34% for testing). Then it trains a classifier using the train data and test it on the test data.

**Stratification:** the class distribution in the original data is preserved in both the training data and the test data.

![[Screenshot 2023-11-15 at 4.47.08 PM.png|500]]

#### Repeated Hold-out method

The hold-out method is unstable due to random sampling!!!
-> To reduce the variability one can average performance across multiple repetitions of the hold-out method

![[Screenshot 2023-11-15 at 4.52.18 PM.png|400]]

**Problems with repeated hold-out method**

- Different training sets overlap. Hence, some instances are used only for training!
- Different test sets overlap. Hence, some instances are used only for testing!
- We need a validation method s.t. any instance to be used at least ones for training and testing.

