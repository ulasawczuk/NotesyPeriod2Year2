
> *k-fold cross-validation* avoids overlapping test sets:
> 	- First step: data is split into *k* subsets of equal size
> 	- Second step: each subset in turn is used for testing and the remainder for training.

The subsets are stratified before the cross-validation.

![[Screenshot 2023-11-15 at 4.56.29 PM.png|300]]

#### Stratification

When splitting the data into train and test sets, it is possible that the instances are not distributed in a balanced way.

![[Screenshot 2023-11-15 at 4.57.40 PM.png|500]]

**Solution:** Stratification tries to maintain similar class balance across splits

MOre info :DDD
- A good split keeps the ratio (Stratification tries to maintain similar class balance across splits)
- Standard method for validation: stratified 10-fold cross-validation
- 10 seems to have the best bias-variance trade-off of estimating the performance measures
- Note that the stratification enhances the estimate's accuracy
- To enhance accuracy further you can use repeated stratified cross-validation