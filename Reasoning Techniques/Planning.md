> Planning is the process of creating a sequence of actions to achieve agent's goal.

Search-based problem-solving agent from lecture 1 is a planning agent.  
Why not use search to perform planning?

---
#### Search vs planning

Consider the task to get milk, bananas and a cordless drill.
Standard search algorithm seems to fail miserably:

![[Screenshot 2023-12-02 at 2.25.08 PM.png|400]]

After-the-fact heuristic/goal test is inadequate.

> Planning systems do the following:

1. 'Open up' action, goal and state representation to allow selection
![[Screenshot 2023-12-02 at 2.27.04 PM.png|400]]
e.g *Buy(x)* causes *Have(x)* $\rightarrow$ If *Have(Milk)* is part of a legal goal, consider action *Buy(Milk)* in the plan.
2. Divide-and-conquer by subgoaling
e.g *get bananas* and *get cordless drill* are independent subproblems
3. Relax requirement for sequential construction of solutions.
e.g action *Buy(Milk)* can be added to the plan before deciding where to buy milk

----
#### PDDL

> PLANNING DOMAIN DEFINITION LANGUAGE

Derived from the original STRIPS planning language, but less restricted (allows negative literals in preconditions and goals).

1. <font color="#76923c">STATE</font>: conjunction of fluents (sentence that can change its truth value) taht are ground (without variables), functionless atoms
e.g state in the shopping problem:
*At(home) $\wedge$ Sells(SM, Milk) $\wedge$ Sells(SM, Bananas) $\wedge$ Sells(HWS, Drill)*

- **Closed-world assumption** = any fluents that are not mentioned are false $\rightarrow$ no need for negations
- **Unique names assumption** = two constants always indicate two different objects

2. <font color="#76923c">ACTIONS</font>: set of action schemas that implicitly define the **ACTIONS(s)** and **RESULT(s,a)** functions needed to do a problem-solving search.

PDDL specifies result of an action in terms of what changes.

**Action schema** - example (assume $\forall$ for variables): 
*Action(Buy(x))*,
PRECONDITION: *At(p) $\wedge$ Sells(p,x)*
EFFECT: *Have(x)*

Ground action resulting from variable substitution:  
*Action(Buy(Milk))*,  
PRECONDITION: *At(SM) $\wedge$ Sells(SM, Milk)*  
EFFECT: *Have(Milk)*

![[Screenshot 2023-12-02 at 2.44.08 PM.png|150]]

- <span style="background:rgba(163, 67, 31, 0.2)">Precondition</span>: conjunctions of literals (positive or negative atomic sentences) - defines the states in which the action can be executed
- <span style="background:rgba(163, 67, 31, 0.2)">Effect</span>: conjunction of literals (positive or negative atomic sentences) - defines the result of executing the action.

An action $a$ can be executed in state $s$ if $s$ entails the precondition of $a:(a \in ACTIONS(s)) \leftrightarrow s | PRECOND(a)$, where any variables in $a$ are universally quantified.

The **result** of executing action $a$ in state $s$ is defined as state $s'$ which is represented by the set of fluents formed by starting with $s$, removing the fluents that appear as negative literals in the action's effects ($EFFECT^-(a)$) and adding the fluents that are positive literals in the action's effects ($EFFECT^+(a)$):
$$s' = RESULT(s,a) = (s- EFFECT^-(a)\cup EFFECT^+(a))$$

3. <font color="#76923c">GOAL</font>: conjunctions of literals (positive or negative) that contain variables.
e.g $At(home) \wedge Have(Milk) \wedge Have(Bananas) \wedge Have(Drill)$

A problem is solved when we can find a sequence of actions that end in a state $s$ that entails the goal.

4. <font color="#76923c">PLAN</font>: data structure consisting of the following four components: 
- Set of plan steps, i.e. actions of the problem
- Set of step-ordering constraints; $S_i ≺ S_j$ ($S_i$ before $S_j$), i.e., step $S_i$ must occur sometime before step $S_j$
- Set of variable-binding constraints: $v = x$ (v = variable in some step, x = either a constant or another variable)
- Set of casual links, $S_i \rightarrow S_j$ ($S_i$ achieves $c$ for $S_j$) i.e. the purpose of $S_i$ in the plan is to achieve precondition $c$ for $S_j$

---
#### EXAMPLE: the blocks world

![[Screenshot 2023-12-02 at 3.09.49 PM.png|400]]

**Initial state?**
$$Init(𝑂𝑛(𝐴, 𝑇𝑎𝑏𝑙𝑒)\wedge 𝑂𝑛(𝐵, 𝑇𝑎𝑏𝑙𝑒)\wedge 𝑂𝑛(𝐶, 𝐴) \wedge 𝐵𝑙𝑜𝑐𝑘(𝐴)\wedge 𝐵𝑙𝑜𝑐𝑘(B)$$$$\wedge 𝐵𝑙𝑜𝑐𝑘(𝐶) \wedge 𝐶𝑙𝑒𝑎𝑟 (𝐵) \wedge 𝐶𝑙𝑒𝑎𝑟 (𝐶) \wedge 𝐶𝑙𝑒𝑎𝑟 (𝑇𝑎𝑏𝑙𝑒))$$
**Goal?**
$$Goal(On(A,B)\wedge On(B,C)))$$
**Actions?**

![[Screenshot 2023-12-02 at 3.13.39 PM.png|300]]

----
#### Partially ordered plans

<font color="#76923c">Partially ordered</font> collection of steps where:
- <font color="#76923c">Start step</font> has the initial state description as its effect
- <font color="#76923c"> Finish step</font> has the goal description as its precondition
- <font color="#76923c">Causal links</font> connect outcome of one step to precondition
- <font color="#76923c">Temporal ordering</font> is specifies between pairs of steps

Some definitions:
- <font color="#76923c">Open condition </font>= precondition of a step not yet casually linked
- A plan is <font color="#76923c">complete</font> iff every precondition is achieved
- A precondition is <font color="#76923c">achieved</font> iff it is the effect of an earlier step and no possibly intervening step undoes it

----
#### Example

![[Screenshot 2023-12-02 at 3.27.50 PM.png|250]]|![[Screenshot 2023-12-02 at 3.31.17 PM.png|250]]
![[Screenshot 2023-12-02 at 3.32.46 PM.png|250]] |![[Screenshot 2023-12-02 at 3.33.11 PM.png|250]]
![[Screenshot 2023-12-02 at 3.34.30 PM.png|250]] Threat!!!!

---
#### Threats and demotion/promotion

The actions $Go(SM)$ and $Buy(Drill)$ threaten each other, because one is removing the precondition of the other.
Casual links in a partial plan are <font color="#76923c">protected links</font>.
<font color="#76923c">Threats</font> = steps that might delete (or clobber) the protected condition.
A casual link is <font color="#76923c">protected</font> by ensuring that threats are ordered to come before or after the protected link.

![[Screenshot 2023-12-02 at 3.38.40 PM.png|250]]

<font color="#76923c">Demotion</font>: put $S_k$ before $S_i$ 
<font color="#76923c">Promotion</font>: put $S_k$ after $S_j$

---
#### Back to example

![[Screenshot 2023-12-02 at 3.40.08 PM.png|250]]
Only promotion is possible: $Go(SM)$ should go after $Buy(Drill)$
![[Screenshot 2023-12-02 at 3.41.46 PM.png|250]]

Going further:
![[Screenshot 2023-12-02 at 3.42.29 PM.png|250]]|![[Screenshot 2023-12-02 at 3.43.18 PM.png|250]]

**Finally**:
![[Screenshot 2023-12-02 at 3.43.59 PM.png|250]]

----
#### Planing process: backtracking search

![[Screenshot 2023-12-02 at 3.45.08 PM.png|300]]

Search in the space of partial plans with operators:
- Add a link from an existing action to an open condition
- Add a step to fullfill an open condition 
- Order one step with another to remove possible threats 

Gradually move from incomplete/vague plans to complete, correct plans.
Backtrack if open condition is unachievable or if threat is unresolvable.

---
#### POP Algorithm

![[Screenshot 2023-12-02 at 6.01.04 PM.png|350]]
![[Screenshot 2023-12-02 at 6.01.35 PM.png|350]]

**Properties of POP**

Backtracks at choice points on failure:
- choice of $S_{add}$ to achieve $S_{need}$ 
- choice of demotion or promotion for threatening operators
- selection of $S_{need}$ is irrevocable

POP is sound, complete, and systematic (no repetition).
Can be made efficient with good heuristics derived from problem description.
Particularly good for problems with many loosely related subgoals.

---
#### Planning in the real world

The planning method that we have seen so far is applicable to fully observable, deterministic, static environments. 
What about partially observable, non-deterministic, and unknown environments?

e.g. flat tire problem:

![[Screenshot 2023-12-02 at 6.05.44 PM.png|300]]

THINGS GO WRONG!

**Incomplete information**
Unknown preconditions, e.g. $Intact(Spare)$?
Disjunctive effects, e.g. $Inflate(x)$ causes $Inflated(x)\vee SlowHiss(x)\vee Burst(x)\vee BrokenPump \vee ...$\

**Incorrect information**
Current state incorrect, e.g. spare NOT intact.
Missing/incorrect post-conditions in operators.

**Qualification problem:**
Can never finish listing all the required preconditions and possible conditional outcomes of actions.

##### Solutions

<u>Conformant or sensorless planning</u>
- For environment with no observations
- Devise a plan that works regardless of state outcome
- Such plans may not exist!

<u>Contingency or conditional planning</u>
- For partially observable and non-deterministic environments
- Plan to obtain information (sensing actions)
- Sub-plan for each contingency, e.g. \[$Check(Tire1)$ if $Intact(Tire1)$ then $Inflate(Tire1)$ else $CallAAA$] 
- Expensive because it plans for many unlikely cases

<u>Online replanning with monitoring</u>
- For unknown environments
- Assume normal states, outcomes
- Check progress during execution (monitoring), replan if necessary
- Unanticipated outcomes may lead to failure

> Really need a combination; plan for likely/serious eventualities, deal with others when they arise, as they must eventually

---
#### Summary

- <font color="#76923c">Planning systems</font> operate on explicit propositional or relational representations of states and actions.
- <font color="#76923c">PDDL</font>, the Planning Domain Definition Language, is used to define the problem.
- The <font color="#76923c">POP algorithm</font> explicitly searches through the space of partially ordered plans.
- Many <font color="#76923c">real-world domains</font> violate the assumption of complete and correct information and deterministic fully observable environments.
	- Conformant plans for environments with no observations
	- Contingent plans for partially observable and nondeterministic environments
	- Online replanning with monitoring to recover from unexpected situations