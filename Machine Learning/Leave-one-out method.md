
>A particular form of cross-validation:
>Set number of folds to number of training instances, i.e. for $n$ training instances, build classifier $n$ times

* Makes best use of the data
* Involves no random sub-sampling
* Very computiationally expensive

#### Stratisfaction

A disadvantage of Leave-One-Out-CV is that stratification is not possible:
-> It guarantees a non-stratified sample because there is only one instance in the test set!

Extreme example: Majority Vote classifier in a balanced 10 pebble data set:
-> "Train” the classifier on all but one instance: It will classify every instance as belonging to blue and be correct 5/9 times on the train data but incorrect 1/1 times on the test data.  
