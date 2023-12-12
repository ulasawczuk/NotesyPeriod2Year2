#### Introduction to Prolog

##### Logic programming and Ordinary programming

|  Logic    |  Ordinary    |
|:-----|:-----|
|  Identify problem    |  Identify problem     |
|  Assemble information    |  Assemble information    |
| Tea break     | Figure out solution     |
|  Encode information in KB    | Program solution     |
|  Encode problem instance as facts    |  Encode problem instance as data    |
| Ask queries     |  Apply program to data    |
|  Find false facts    |   Debug procedural errors   |
| **DECLERATIVE**   | **PROCEDUAL**     |

##### Prolog systems

**PROLOG:** became popular in Europe, most widely used logic programming language

**Basis:** backward chaining with Horn clauses + bells & whistles

**Program:** set of clauses = head :− literal$_1$ , ... literal$_n$
e.g. $American(x)\wedge Weapon(y)\wedge Sells(x,y,z)\wedge Hostile(z)\rightarrow Criminal(x)$
	criminal(X) :− american X , weapon(Y), sells(X, Y, Z), hostile(Z)

**Characteristics:**
- Efficient unification 
- Efficient retrieval of matching clauses 
- Depth-first, left-to-right backward chaining  
- Built-in predicates for arithmetic etc., e.g., $X$ is $Y ∗ Z + 3$  
- Closed-world assumption (“negation as failure”) 
	- What is not known to be *true*, is *false*

----
##### Example
Family relations:

![[Screenshot 2023-11-21 at 11.13.47 AM.png|300]]

Queries recap:
- ?- parent(tom,bob).  
- ?- parent(liz,pat).  
- ?- parent(X,liz).  
- ?- parent(X,bob).  
- ?- parent(bob,X).  
- ?- parent(X,Y).  
- ?- parent(X,jim), parent(X,Y).  
- ?- parent(X,ann), parent(X,pat).  
- ?- parent(tom,bob).  
- ?- parent(tom,bob).

----
#### Syntax and meaning of Prolog programs

##### Types of clauses

> 1. Facts

- with <font color="#c0504d">head</font> but no <font color="#4f81bd">body</font>;  
- unconditionally true;  
- e.g. <font color="#c0504d">parent(bob, pat) </font> 

> 2. Rules  

- with <font color="#c0504d">head</font> and <font color="#4f81bd">body</font>;  
- conditionally true;  
- e.g. a<font color="#c0504d">ncestor(X,Z)</font> :- <font color="#4f81bd">parent(X,Y), parent(Y,Z)</font>  

>1. Queries  

- with <font color="#4f81bd">body</font> but no head; 
- trueness to be deduced;  
- e.g. <font color="#4f81bd">ancestor(pam,X)</font>

#####  Data objects 

![[Screenshot 2023-11-21 at 11.18.15 AM.png|400]]

> Prolog recognizes the type of an object from its syntax $\rightarrow$ no need to specify data types (like e.g. in Java)

##### How does Prolog answer queries?

Prolog as a theorem prover. Example goal:  
-> ?- ancestor(tom,pat).

```
parent(tom,bob).  
parent(tom,liz).  
parent(bob,pat).  

...  
% Rule al:  
ancestor(X, Z) :-  
	parent(X, Z).  
	
% Rule a2:  
ancestor(X, Z) :-  
	parent(X, Y),  
	ancestor(Y, Z).
```

![[Screenshot 2023-11-21 at 11.20.31 AM.png|300]]

This is backwards chaining!!

##### Matching

**Matching** = process that takes as input two terms and checks whether they match. It’s used by Prolog to prove facts with backward chaining.

Two terms match if:  
1. they are identical, or  
2. the variables in both terms can be instantiated such that the terms can be made identical

For example, the two terms :
	ancestor(tom, pat) and ancestor(X, Y)  
match under the instantiation : 
	X = tom  
	Y = pat

##### Ordering of clauses and goals

Consider the following variations of the ancestor relation:

![[Screenshot 2023-11-21 at 11.30.52 AM.png|250]]

What happens if we query Prolog with anc(tom, pat)?
anc1(tom,pat), Backward chaining:

![[Screenshot 2023-11-21 at 11.31.50 AM.png|300]]

anc2(tom,pat), Backward chaining:

![[Screenshot 2023-11-21 at 11.33.25 AM.png|350]]

anc3(tom,pat), Backward chaining:

![[Screenshot 2023-11-21 at 11.34.21 AM.png|250]]

anc4(tom, pat), Backward chaining:

![[Screenshot 2023-11-21 at 11.35.06 AM.png|300]]

General practical heuristics in problem solving:  
- Heuristic 1:  
	- *It is sensible to put the simplest clause first*

A recursive goal is less simple than a non-recursive goal, so:  
-  Heuristic 2:
	- *It is sensible to put the simplest goal first*
---
#### Lists, operators, arithmetic

##### Lists
List in Prolog notation:

![[Screenshot 2023-11-21 at 11.38.33 AM.png|200]]

Empty list: \[]
Other notation:
- \[ Head1 | Tail ]
- \[ Head1, Head2 | Tail ]
in which Head1 etc. is/are one or more elements and Tail is a list.

> Remember that this notation is **syntactic sugar**. Internally, Prolog  represents lists using the functor “.”:  
> .(coffee, .(tea, .(water, .(beer, .(juice, \[ ])))))

**Operations on lists:**

The most important list **operations**:  
- **Adding** an object to a list  
- **Deleting** an object from a list  
- Checking for **membership**  
- **Concatenation** of two lists  
- Determining **sublists** of a list  
- Obtaining **permutations** of a list  

Prolog may have primitive (pre-defined) functions, but this strongly depends on the Prolog system used. We can always define functions ourselves and store them as a kind of library.  

**Some examples:**

- Adding an object to a list with add/3 (no need for a rule, the following fact is sufficient): $$add(X, L, [X | L])$$
- Deleting an object from a list with del/3: $$del(X, [X | Tail], Tail).$$$$del(X, [Y | Tail], [Y | Tail1]) :-  
del(X, Tail, Tail1)$$
- Example: $$del(a, [a,b,a,a], L).$$$$L = [b,a,a];$$
$$L = [a,b,a];$$$$L = [a,b,a];$$$$no$$
- Checking list membership: how it should work $$?- member(b, [a,b,c]). \rightarrow yes$$$$?- member(b, [a, [b,c]]).\rightarrow no$$$$?- member([b,c], [a, [b,c]]).\rightarrow yes$$
So, $member$ should be a function that checks for “direct”  
membership of “arbitrary” objects.

Recursive definition of $member/2$:  
	member(X, \[X | Tail]).  
	member(X, \[Head | Tail]) :-  
		member(X, Tail).

##### Operators

Prolog uses **structures** for mathematical expressions (“functions”).  
An expression like $$2×𝑥 + 𝑦×𝑧$$  
can be represented in Prolog by  
$$+( *(2,X), *(Y,Z))$$
However, Prolog allows the infix notation for some operators, allowing the  
expression to be written as:  
$$2*X + Y*Z$$ 
The ‘$*$’ (multiplication) operator of course binds “stronger” than the ‘+’  
(addition), which is defined by Prolog’s precedence. The principal functor  
(weakest binding) has the highest precedence. So  
$$X + Y * Z$$  
means in Prolog: $+(X, *(Y,Z))$, with principal functor +,  
and not $*(+(X,Y), Z)$ 
In the latter case, use parentheses: $(X + Y) * Z$

##### Aritmetic

Prolog offers predefined operators for doing arithmetic:
- + addition
- - subtraction
- $*$ mulitplication
- $**$ power
- / division
- $mod$ modulo, the ramainder if integer division

However, the computation is not “ automatic”:$$?- X = 1 + 2.$$  
$$X = 1 + 2$$
So, $1 + 2$ is just a structured term and $X$ matches that term.  
To force computation:$$?- X is 1 + 2.$$  
$$X = 3$$
The infix operator $is/2$ first evaluates the right-side term by calling built-in procedures before matching. 

>Note that all variables must be instantiated to numbers at the time of evaluation!

Also comparisons invoke evaluation, in this case of both the left-hand side and the right-hand side of the expression: $$?- 277 * 37 > 10000 - 1.$$
Yes, since $277*37=10249$

The comparison operators:
- $X > Y$
- $X < Y$
- $X >= Y$
- $X <= Y$
- $X =:= Y$
- $X =\= Y$
---
#### Summary

- Prolog programming consists of defining relations and querying about relations.  
- A program consists of clauses of three types: facts, rules and queries.  
- To answer a query, Prolog performs inference using backward chaining and matching to find all instantiations of variables that satisfy the query.  
- The order in which goals and clauses are defined can affect the efficiency of the program.  
- Lists are a frequently used structure and Prolog provides a special notation for them.  
- Prolog allows to define operators and provides built-in arithmetic procedures.

