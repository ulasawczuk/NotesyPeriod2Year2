#### B.

![[Pasted image 20231120202414.png|500]]

From plots above we can see that after normalization both the training and hold-out (test) accuracy rates improved. Noticing that the accuracies are higher in the plot with normalized indicates  that our model is performing better on not yet seen data when it is trained with normalized data (on which it learns better). So yes! Normalizing the data will improve both training and test accuracy! (Of course it is in our case, it always good to practice)

Here is the plot for diabetes data set:
![[Pasted image 20231120215626.png|500]]

Here the better outcome after normalizing is not seen as good as before also noticing that our average test accuracy is 0.7082538167938931 and normilized average test accuracy is a tiny bit lower , 0.7077767175572519 does not completely satisfy my answer from above. However, I was able to run the code on diabietes data set only once as it run for 77 minutes:

![[Screenshot 2023-11-20 at 10.01.18 PM.png|400]]
proof:D
But I stick to my intuition and knowledge that usually normalizing the data will obtain us better outcomes.

![[Pasted image 20231120221506.png|500]]

The $exp$ component is used in calculations of the Minkowski distance and it can affect the performance of the classifier. When $exp=1$ the Minkowski distance is equal to Manhattan distance, when $exp=2$ it is equal to Euclidean distance and for other values it is a different calculation lying somewhere between the Manhattan and Euclidean distance. In our case we clearly see that the performance is drooping as $exp$ grows. 

#### C.
![[Screenshot 2023-11-20 at 11.11.25 PM.png|600]]
![[Screenshot 2023-11-20 at 11.14.54 PM.png|600]]

These are my outputs for the C part, here we can see the probabilities of each instance for each class and its real class.

#### D.
![[Pasted image 20231120231652.png|500]]

Here is my output for the d part. 