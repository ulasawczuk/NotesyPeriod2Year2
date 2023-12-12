##### Mathematical model of Queueing Systems

* customer/jobs
* arrival process: inter-arrival time distribution (A)
* servers: service time distribution (S), number of servers (N)
* queue: capacity (k), discipline (FCFS, LCLS, SIRO, Priority)

![[Screenshot 2023-11-06 at 9.07.57 PM.png|300]]
Notation: A|S|N|k 
Standard notation for distributions:
* D: deterministic
* M: exponential
* $E_k$: erlang-k
* N: gaussian
* G: general (service time)
* GI: general independent (inter-arrival time)

**Examples:**
Single server with exponential inter-arrival time and exponential service time: M|M|1 (short for M|M|1|$\infty$, infinity always where not specified)
Three servers with exp. inter-arrival and exp. service time, total capacity of 3: M|M|3|3

**Arrival process**
Describe how customers enter a system 

![[Screenshot 2023-11-06 at 4.58.06 PM.png|300]]

**Counting process**
A stochastic process, {$N(t), t \geq 0$}, that represents the number of 'events' up to time $t$ is called a *counting process*.
A counting process, {$N(t), t \geq 0$}, satisfies:
1. $N(t) \geq 0$
2. $N(t)$ is integer valued
3. If $s < t$ then $N(s) \leq N(t)$
4. For $s < t$, $N(t) - N(s)$ equals the number of 'events' that occur in the interval ($s,t$]

![[Screenshot 2023-11-06 at 5.04.19 PM.png]]

**Properties of counting process**
* Independent increments if, given $t_1 < t_2 < t_3$, $N(t_2 - t_1)$ and $N(t_3 - t_2)$ are independent
* Stationary increments if the distribution of $N(t+s)-N(s)$ is independent of $s$
