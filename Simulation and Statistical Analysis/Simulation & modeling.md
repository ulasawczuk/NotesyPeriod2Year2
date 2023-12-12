+ ##### Simulation
The use of computer techniques to simulate a real world facility or process (the system).

+ ##### Model
Mathematical or logical representation of system behaviour (we want to see and know what's up). Defined by known relationships. **It's evaluated numerically during simulation.**

#### ==Models, Simulations and Systems==

+ ##### Mathematical model
Representation of essential aspects of an existing system (or one to be constructed) which presents the knowledge of the system in a usable form. (smart representation of the thing)

+ ##### State
Collection of variables representing the current state of the system at a particular time. (the state of the thing)

+ ##### System
Collection of entities that act and interact together to the accomplishment to a logical end. (the thing and small things making it)

**- Types of systems**
*Discrete:* State variables change  separated points in time
*Continuous:* State variables change continuously with time

**- Types of models**
*Static / Dynamic
Deterministic / Stochastic
Continuous / Discrete*

![[Screenshot 2023-11-01 at 1.27.37 PM.png|400]]

**Example:** Modelling illness
How do disease treatments affect life expectancy?

![[Screenshot 2023-11-01 at 1.28.56 PM.png|400]]

**- Types of simulations**
*[[Monte Carlo simulation]]
[[Continuous simulation]]
[[Discrete Time simulation]]
[[Discrete Event simulation]]

#### ==Modeling==
* Activity-based
* Event-based
* Process-based

**Example:** Restaurant Extension "Il Giardino"
* Tables of 2
* 20 tables
* Customer will wait if no more than 2 customers are already waiting
* Timeless arrivals

Components:
* Customer (temporary, component class)
* Queue (permanent)
* Restaurant (permanent)
Variables:
* Neating
* Nqueue
* TarrivalCust
* TdepartureCust
* Ncustomers
* NwalkBy
* CurrentTime

![[Screenshot 2023-11-02 at 5.58.57 PM.png|400]]

**Activity based description**
We can look at the activities: arrivals, walkbys, queuins, queueouts, departures. In activity based, we just check if the conditions are satisfied.

IF currentTime == TarrivalCust$_i$ THEN arrival
IF currentTime == TarrivalCust$_i$ AND Nqueue == 3 THEN walkBy
IF currentTime == TarrivalCust$_i$ AND Nqueue < 3 THEN queueIn
IF currentTime == TarrivalCust$_i$ AND Neating < 20 THEN queueOut
IF currentTime == TdepartureCust$_i$ THEN departure
IF currentTime == TdepartureCust$_i$ AND Nqueue > 0 THEN queueOut

![[Screenshot 2023-11-02 at 6.06.56 PM.png|400]]

**Process based description**
Here we model things based on the perspective of components. We can assign arrivals and a walkby to the customer component. We can give a queuein can be handled by a queue while a queueout and the departure can be handled by the restaurant. The restaurant knows when to kick ppl out. In the diagram the dashed lines represent "messages".

![[Screenshot 2023-11-02 at 6.07.11 PM.png|400]]

![[Screenshot 2023-11-02 at 6.07.29 PM.png|400]]

**Event based description**
Our two events are arrival and departure. The added benefit is that we know at what time these events will happen. This means we do not have to have fixed time steps checking whether things happened, but rather we can just jump from event to event, hence [[Discrete Event simulation]]. 

![[Screenshot 2023-11-02 at 6.11.04 PM.png|400]]