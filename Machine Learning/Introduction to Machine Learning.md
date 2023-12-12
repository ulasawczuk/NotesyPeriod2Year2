**What is machine learning?**
Machine learning is a scientific discipline that deals with developing computer systems that automatically improve with experience.
In addition, machine learning aims at discovering the fundamental laws that govern all learning processes.

**When do Programs Learn?**
A computer program is said to *learn* from experience $E$ with respect to some class of tasks $T$ and performance measure $P$, if its performance at tasks in $T$, as measured by $P$, improves with experience $E$.

----
#### Well-Posed Learning Problems

A learning problem is said to be well-posed if and only if the class of tasks $T$, the performance measure $P$, and the experience $E$ are determined.

A checkers learning problem  
* T = playing checkers  
* P = percent of games won in a tournament 
* E = games played against self

A hand-writing recognition learning problem  
* T = recognizing handwritten words within images  
* P = percent of words correctly classified  
* E = database of handwritten words with given classifications  

A robot driving learning problem  
* T = driving on highways using vision sensors  
* P = average distance traveled before an error  
* E = sequence of images and steering commands recorded while observing a human driver

---
#### Three Niches for Machine Learning

1. Data mining: using historical data to improve decisions:  
	* medical records à medical knowledge.  
2. Software applications we can't program:  
	* autonomous driving;  
	* speech recognition.  
3. Self-improving programs:  
	* newsreader that learns user interests;  
	* online shops that learn user preferences.

**Example of a Data Mining task**

![[Screenshot 2023-11-07 at 1.50.52 PM.png|200]]
Given:  
*  9714 patient records  
* Each patient record contains 215 features  

Learn to predict:  
*  Future patients at high risk for Emergency Cesarean Section  

A possible rule learned is that one:  
If No previous vaginal delivery, and Abnormal 2nd Trimester Ultrasound, and Malpresentation at admission Then Probability of Emergency C-Section is 0.6.

---
**Designing a System that Learns to Play Checkers** 

The learning problem is defined as follows:
* T = playing checkers
* P = percent of games won in tournament
* E = games played against self()

Questions to be answered:
* Exactly what is given, what is learned, what representation and learning algorithm should we use

1. **What do we learn?**
Given board situation, which move to make

2. **What is given?**
Direct or indirect evidence?
* direct e.g. which moves were good, which were bad  
* indirect: consecutive moves in game, + outcome of the game
In our case: **indirect** evidence (direct evidence would require a teacher)

3. **What exactly shall we learn?**
Choose **type** of target function:
* ChooseMove: Board -> Move 
	* directly applicable
* V: Board -> Score
	* indicates quality of state  
	* when playing, choose move that leads to best state

>Note: reasonable definition for V easy to give:
>V(won) = 100, V(lost) = -100, V(draw) = 0, for any other state s: V(s) = V(e) with e is the best state reachable from s when playing optimally. Not feasible in practice

Since we can't have the ideal target function $V$, we try to design an approximation $V'$.
Choose **representation** for the approximation $V'$:
* set of rules?
* neural network?
* polynomial function of numerical board features?
* ...
Let's choose!:
$$V' = w_1bp + w_2rp + w_3bk + w_4rk + w_5bt + w_6rt$$
where,
* $bp, rp =$ number of black/red pieces
* $bk, rk =$ number of black/red kings  
* $bt, rt =$ number of black/red pieces threatened
* *$w_i:$ constants to be learned from experience

4. **How to obtaining training examples?**
We need a set of examples $[bp, rp, bk, rk, bt, rt, V]$.
$bp$ etc. easy to determine, but how to guess $V$?
We have indirect evidence only!:0

**Possible method**:
With $V(s)$ true target function, $V’(s)$ learned function,  $V_t (s)$ training value for a state $s$:
$$V_t(s) \leftarrow V'(siccessor(s))$$
**Intuitively**: $V$ for end states is known; propagate $V$ values from later states to earlier states in the game.

![[Screenshot 2023-11-09 at 12.00.36 PM.png|400]]
![[Screenshot 2023-11-09 at 12.24.36 PM.png]]

---
#### Adjusting the weights

Training algorithm: how to adapt the weights $w_i$?
Possible method:
* look at “error”: $error(s) = V’(s) - V_t (s)$
* adapt weights so that error is reduced  
* e.g. using gradient descent method  
	* for each feature $f_i : w_i \leftarrow w_i + c f_i error(s)$ with $c$ some small constant
---
#### Final System Design

![[Screenshot 2023-11-09 at 12.29.00 PM.png|300]]

---
#### Design Choices

![[Screenshot 2023-11-09 at 12.29.22 PM.png|300]]

---
#### Tasks in Machine Learning

* [[Classification task]]
* [[Regression task]]
* [[Clustering task]]
* Reinforcement Learning Task
* And manyyyy more....

---
#### Some current research questions
* Can unlabeled data be helpful for learning?  
* How can we transfer what is learned for one task to improve learning in other related tasks?  
* What is the relationship between different learning algorithms, and which should be used when?  
* For learners that actively collect their own training data, what is the best strategy? 
* To what degree can we have both data privacy and the benefits of data mining?

---
#### Long-term research questions
* Can we build never-ending learners? 
* Can machine learning theories and algorithms help explain human learning?  
* Can we design programming languages containing machine learning primitives?

---
#### Summary

* Machine learning deals with developing systems that automatically improve with experience.  
* Machine Learning has a great practical value.  
* Machine Learning is based on a set of disciplines like CS, AI, Statistics, etc.  
* Designing a Machine Learning systems involves a number of design choices.