[[Queueing Systems]]

Main idea of a *Poisson process* is that events occur over time or space in a random fashion.
We can model it as $Bin(n,p)$, where $n$ is the number of time intervals (how many minutes, hours etc.) and $p$ is the probability of an arrival at each time interval.
We want $n$ to be large -> then $p$ will be smaller, as $\lambda = np$ is being held constant at $\lambda$ customers per hour.
As $n -> \infty$ the number of arrivals during the hour ~ $Poisson(\lambda)$
! The probability of two or more arrivals occurring at the same time in a Poisson process is 0 (because time is continuous)
##### Two Poisson process definitions
A counting process {$N(t), t \geq 0$} is said to be a *Poisson process* with rate $\lambda, \lambda >0$, if

**Def 1**
1. $N(0) = 0$ (if no time has passed no events are generated)
2. Has independent increments
3. The number of events in any interval of length $t$ is $Poisson(\lambda t)$ distributed (with mean $\lambda t$). That is for all $s, t \geq 0$.
$P(N(t+s)-N(s)=n)=e^{-\lambda t}\frac{(\lambda t)^n}{n!}$ , n= 0,1,2,... (specific number of arrivals)

**Def 2**
1. $N(0) = 0$
2. Has stationary and independent increments
3. Arrivals occur at separate moments in time (there are no two simultaneous arrivals at any time $t$) (this is because it is binomial as $n -> \infty$ if we divide intervals $t$ into $n$ equal bins)

**Equivalence of the definitions**

From def 1 -> def 2
2. stationary increments: $N(t +s) -N(s)$ is independent of $s$.
3. $P(N(t+s)-N(s)=k)=e^{-\lambda t}\frac{(\lambda t)^k}{k!}$
$$\lim_{h->0}P[N(h)\geq 2] = \lim_{h->0}(1- P[N(h)=0]-P[N(h)=1]) = \lim_{h->0}(1 - e^{-\lambda h}(=1) - \lambda h e^{-\lambda h}(=0))=0$$

From def 2 -> def 1
3. Divide interval \[0, 𝑡) into $𝑛$ equal bins. For $n -> \infty$, 3. implies 0 or 1 arrival per bin. With rate $\lambda$, probability of arrival in a bin is $\frac{\lambda t}{n}$.

![[Screenshot 2023-11-07 at 3.34.46 PM.png|300]]

From this we can derive $N(t) \sim Bin(n, \frac{\lambda t}{n})$ as $n -> \infty$
So, $$P[N(t) = k] = \lim_{n->\infty}{n\choose k}(\frac{\lambda t}{n})^k(1-\frac{\lambda t}{n})^{n-k} = \lim_{n->\infty}\frac{n(n-1)...(n-k+1)}{k!}\frac{(\lambda t)^k}{n^k}\frac{(1-\frac{\lambda t}{n})^n}{1-\frac{\lambda t}{n})^k}$$
Because $$lim_{n->\infty}\frac{n(n-1)...(n-k+1)}{k!} = 1, \lim_{n->\infty}(1+ \frac{x}{n})^n = e^x, \lim_{n->\infty}(1+ \frac{x}{n})^k = 1$$
We get $$P[N(t) = k] = e^{-\lambda t}\frac{(\lambda t)^k}{k!}$$
Combining this finding with 2. we find $$P(N(t+s)-N(s)=k)=e^{-\lambda t}\frac{(\lambda t)^k}{k!}$$
##### Poisson Process and The Exponential Distribution

[[Exponential Distribution]]
**Recap:**
Let $X \sim Exp(\lambda)$, then

Property|Property
---|---
$f(x)$ | $\lambda e ^{-\lambda x}$
$F(x)$ | $1 - e ^{-\lambda x}$
$P(X \geq x)$ | $e ^{-\lambda x}$
$E[X]$ | $\frac{1}{\lambda}$
$Var(X)$ | $\frac{1}{\lambda^2}$

**Memoryless property**
Let $X \sim Exp(\lambda)$, it holds that $$P(X \leq x + t | X \geq x) = P(X \leq t)$$![[Screenshot 2023-11-07 at 4.02.27 PM.png|400]]

The probability of an event occurring after a certain interarrival time is independent of the amount of time that has already elapsed. The probability of and event occurring depends only on the amount of time remaining. It is the same regardless of whether the event has already occurred or not. For example, the probability of a lightbulb lasting another hour is the same whether it has already been on for one hour or ten hours.

**Proof**:
$$P(X \leq x + t | X \geq x)  = 1 - P(X \geq x + t | X \geq x) = 1 - \frac{P(X \leq x + t \cap X \geq x)}{P(X \geq x)} = 1 - \frac{P(X \leq x + t)}{P(X \geq x)}$$
$$P(X \leq x + t | X \geq x) = 1 - \frac{e^{-\lambda (x+t)}}{e^{-\lambda x}} = 1 - e^{-\lambda t} = P(X \leq t) $$
**Mathematical model of Arrival Process**
Two ways of looking at the arrival process:
* Number of ‘events’ ($N(t)$)
* Arrival times ($T_n$) and inter-arrival times ($A_n$)

![[Screenshot 2023-11-07 at 4.20.58 PM.png|400]]

**Poisson Process & Exponential Distribution**
Let $T_1$ denote the time of the first arrival

Poisson Process | Exponential Distribution
---|---
Recall, $P[N(t) = n] = e^{-\lambda t}\frac{(\lambda t)^n}{n!}$ | Let $T_1 \sim Exp(\lambda)$, then $P(T_1 \geq t) = e^{-\lambda t}$
Thus, $P(T_1 > t) = P(N(t) = 0) = e^{-\lambda t}$ | Thus, $P(T_1 > t) = P(T_1 \geq t) = e^{-\lambda t}$
number of events in a certain time | time between two consecutive events 

**Inter-arrival times for a Poisson Process**
Let $N(t), t \geq 0$ denote a Poisson Process with rate $\lambda$, then the inter-arrival times ($A_n$) follow  an exponential distribution with parameter $\lambda$.

**Erlang Distribution**
Let $A_1, A_2, ..., A_n \sim Exp(\lambda)$, then $$T_n = \sum_{i=1}^nA_i$$
is called the Erlang distribution (denoted by $E_n(\lambda)$ with PDF: $$f_{T_n}(t) = \lambda e^{-\lambda t}\frac{(\lambda t)^{n-1}}{(n-1)!}$$
Erlang distribution is a sum of exponentials <- $n^{th}$ event times 

**Example**
On average you complete 6 homework problems per hour. 

What is the probability that you complete less than two problem in 20 minutes?
$X =$ number of problems completed in 20 minutes 
$$X \sim Pois(6*\frac{1}{3})= Pois(2)$$
$$P(X \leq 1) = e^{-2}(1+2) = 3e^{-2} \approx 0.406$$
What is the probability that you complete a homework problem between 5 and 8 minutes?
$Y =$ number of minutes between solving problems 
$\lambda = \frac{6}{60} = 0.1$ per minute, $$Y\sim Exp(\lambda) = Exp(0.1)$$
$$P(5 \leq Y \leq 8) = P(Y \leq 8)  - P(Y \leq 5) $$
$$= (1-e^{-0.1*8}) - (1 - e^{-0.1*5}) \approx 0.1572$$ 
#### Properties of Poisson Process

##### Conditioning on number of arrivals 
For a Poisson Process with rate $\lambda$, we know that $N(t) \sim Bin(n, \frac{\lambda t}{n})$ as $n -> \infty$
If in an interval \[0, t) , the number of observed 'events' $N(t) = k$, these $k$ arrivals follow a $U(0,t)$ distribution.

Given that in the interval \[0,t) the number of arrivals is $N(t) = n$, these $n$ arrivals are independently and uniformly distributed in the interval. One way to generate a Poisson process in given interval:
* draw the total number of arrivals $n$ from the Poisson($\lambda$) distribution 
* for each arrival draw its position in the interval \[0,t) from the uniform distribution independently of the others

##### Random selection
Suppose we have a Poisson Process with rate $\lambda$ and we select each arrival with probability $p$.
The result is a Poisson Process with rate $\lambda p$.
This way we can lower the parameter $\lambda$ if we randomly select arrivals. 
This procedure is called a **thinning algorithm** and is used in time-varying Poisson processes (to generate a random variate).

![[Screenshot 2023-11-08 at 12.34.15 PM.png|350]]

##### Superposition
The superposition of two Poisson Processes ($PP(\lambda_1)$ and $PP(\lambda_2)$) constitutes a $PP(\lambda_1 + \lambda_2)$.

This property states that the arrival rate of a Poisson process over a given time interval is the sum of the arrivals rates of the individual processes making up the overall process. It is useful in modelling the arrival of customers to a system, since it is assumed that the arrival of customers from different sources are independent of each other. For example, if a system receives customers from two sources, the arrival rate of customers to the system can be calculated by summing the arrival rates of customers from each source.

![[Screenshot 2023-11-08 at 12.40.07 PM.png|350]]

**Proof:** we focus in the first arrival: $Y = min(X_1,X_2)$
$$P[Y >t ] = P[min(X_1,X_2)>t]$$$$=P[(X_1>t) \cap (X_2 >t)] = P[X_1 >t] * P[X_2 >t]$$
$$= e^{-\lambda_1 t} * e^{-\lambda_2 t} = e^{-(\lambda_1 + \lambda_2)t}$$
Repsectively, $$P[Y \leq t] = 1 - e^{-(\lambda_1 + \lambda_2)t}$$
##### Random Split
$PP(\lambda_1 +\lambda_2)$, the superposition of $PP(\lambda_1)$ and $PP(\lambda_2)$, is randomly split, what is the probability that the arrival belongs to either process?
Condition on $X_1$ $$P(X_1<X_2) = \int_0^\infty P(X_1<X_2 | X_1 = x)* P(X_1 = x)dx$$
$$= \int_0^\infty P(x <X_2)* \lambda_1e^{-\lambda_1 x}dx$$
$$= \int_0^\infty e^{-\lambda_2 x}*\lambda_1e^{-\lambda_1 x} = \int_0^\infty \lambda_1e^{-(\lambda_1+\lambda_2)x}dx$$
$$= \frac{-\lambda_1}{\lambda_1+\lambda_2}e^{-(\lambda_1+\lambda_2)x}|_0^\infty= \frac{\lambda_1}{\lambda_1+\lambda_2}$$
If a Poisson process with intensity $\lambda$ is randomly split into two subprocesses with probabilities $p_1, p_2$, where $p_1+p_2=1$, then the resulting processes are independent Poisson processes with intensities $p_1\lambda,p_2\lambda$. (This result allows a straight forward generalization to a split into more than two subprocesses)

![[Screenshot 2023-11-08 at 4.55.17 PM.png|350]]

**Example**:
A copy shop has two printers ($M_1, M_2$), on which printing times ($S_{M_i}$) follow an exponential distribution. At the moment, both printers are working on a job. From which value of $\lambda$
will $M_2$ be more likely to idle first?
$$S_{M_1} \sim Exp(1), S_{M_2} \sim Exp(\lambda)$$
$$P(S_{M_1} < S_{M_2}) = \frac{\lambda}{1+\lambda}$$$$P(S_{M_2}<S_{M_1})>\frac{1}{1+\lambda}$$
Then $M_2$ is done quicker
$$\frac{\lambda}{1+\lambda}> \frac{1}{1+\lambda} \implies \lambda +\lambda^2 > \lambda +1 \implies (\lambda^2-1)>1$$
Thus, $$\lambda \in (-\infty,1) \cup (1, \infty)$$
But can't be negative so, $$\lambda \in (1, \infty)$$
##### PASTA i basta
The PASTA property refers to the expected state of a queueing system as seen by an arrival from a Poisson Process. An arrival from a Poisson Process observes the system as if it was arriving as a random moment in time. Therefore, the expected value of any parameter of the queue at the instant of a Poisson arrival is simply the long-run average value of that parameter.
For example, at the instant of a Poisson arrival,
* the expected number of customers in the queue, including the one in service, is $\bar{Q}$
* the probability the server is busy is $U$
* the probability the server is idle is $1-U$
* the expected number waiting and not being served is $\bar{Q}-U$

**Steady state analysis**

State: encapsulates system information
![[Screenshot 2023-11-08 at 5.09.19 PM.png|350]]
Steady state probabilities ($\Pi_j$) :  
- Long run probability of being in state 𝑗

Consider the following two long run probabilities when considering a system:
* $\Pi_j$: the probability that an outside observer sees the system in state $S_j$.  
- $\Pi_j^*$: the probability that an arriving customer sees the system in state $S_j$.  
Generally speaking: $\Pi_j$ ≠ $\Pi_j^*$
But not in Poisson proces arrivals!

The probability of the state as seen by an outside random observer is the same as the probability of the state by an arriving customer. Customers with Poisson arrivals see the system as if they came into the system at a random instant of time (despite they induce the evolution of the system).

**Example**: D | D | 1 - queue (single server, deterministic (constant service times and interarrival times))

Suppose we have a single server with customers (with a service time of 1) arriving at $t = 1,3,5, ...$

![[Screenshot 2023-11-08 at 5.19.20 PM.png|350]]
outside observer: $\Pi_j$ 
$\Pi_{busy} = \frac{1}{2}$, $\Pi_{idle}=\frac{1}{2}$, long range average from system's point of view (50%)

In real world:
![[Screenshot 2023-11-08 at 5.23.17 PM.png|350]]
arriving customer: $\Pi_j^*$
$\Pi_{busy}^* = 0$, $\Pi_{idle}^* = 1$, when a customer arrives he never sees a busy server (has different perspective)

**Poisson Process arrivals**
What if the arrivals followed a Poisson Process?
From the property “Conditioning on the number of arrivals”, arrivals occur uniform at random.

![[Screenshot 2023-11-08 at 5.26.48 PM.png|350]]

##### Hitchhiker paradox
* Cars passing point on road according to Poisson process with rate $\lambda$
* Hitchhiker arrives at point at random instant of time  
* Question: What is the average waiting time?

![[Screenshot 2023-11-08 at 5.29.32 PM.png|350]]
$$\bar{W} = \frac{1}{t}\int_0^tW(\tau)d\tau = \frac{1}{t}\sum_{i-1}^n\frac{1}{2}X_I^2 = \frac{1}{n\bar{X}}\sum_{i=1}^n\frac{1}{2}X_i^2$$
$$=\frac{\bar{X^2}}{2\bar{X}} = \frac{\bar{X^2}+ var(X)}{2\bar{X}} = \frac{2\bar{X^2}}{2\bar{X}} = \frac{\bar{X^2}}{\bar{X}} = \bar{X}$$
![[Screenshot 2023-11-08 at 5.45.01 PM.png|350]]
Thus, it's the mean of the interarrival times: $E(Exp(\lambda))= \frac{1}{\lambda}$

**Exercise**:
A restaurant offers two different types of meals to its customers to be delivered at home, being Indonesian cuisine or Chinese cuisine. The orders for both these types of meals are placed according to independent Poisson processes. Orders for meals from the Indonesian cuisine arrive with a rate of 10 per hour.
After an order for a meal from the Indonesian cuisine is placed, it takes on average 5 minutes until a meal from the Chinese cuisine is ordered. What is the arrival rate for orders of Chinese cuisine meals?

Due to Hitchhiker paradox exponential distribution probabilistically restarts after ordering Chinese.
orders:
Indonesian: $I \sim PP(10)$
Chinese: $C \sim PP(?)$
5 minutes occur 12 times in an hour, thus $\lambda_c  =12$ orders per hour.


