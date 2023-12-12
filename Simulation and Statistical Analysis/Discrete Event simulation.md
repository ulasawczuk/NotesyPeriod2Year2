In discrete event simulation:
* The simulated system runs in continuous time
* We need two things:
	* Events
	* Time
---
**Event**: An occurence that may change the system's state
**Simulation clock**: Variable that gives the current value of simulated time (just time of the sim). Can be advanced i.e. Next-time advance, Fixed-increment advance
###### Next-time advance
* Clock initialized to zero
* Times of events are determined
* Clock advanced to time of first event -> system's state updated
* Clock advanced to time of next event -> system's state updated
* Continuous until stopping condition satisfied

###### Fixed-increment advance
* Advancing time in the system by a predefined quantity
* Does not skip over inactive periods
* Can use up a lot of computer time
###### ---

![[Screenshot 2023-11-02 at 5.16.13 PM.png]]



![[Screenshot 2023-11-02 at 5.20.52 PM.png]]

###### Example
Consider the following $D|D|1$ queue, we have custumers ($i$), their arrival time ($A_i$), and service time ($S_i$):
![[Screenshot 2023-11-02 at 5.32.20 PM.png|100]]
Calculate the waiting time ($E(D)$) = delay = service start time - arrival. We often look for an average (an estimate over some n customers).
$d = E(D) = \frac{\sum_iD_i}{234} = \frac{99}{234} = 0.42$ 
Where T = 234, total time in simulation, time of last departure of $i$
$D_i = A_{i-1} + S_{i-1} - (A_{i-1}+A_i)= S_{i-1} - A_i$ for $i >1$, and $D_1 =0$ (no waiting time:))
Now let's calculate $E(W)$
$E(W) = \frac{\sum_i{S_i}+\sum_i{D_i}}{\sum_i{i}} = \frac{176 + 99}{7}$

![[Screenshot 2023-11-06 at 9.22.59 PM.png|500]]

