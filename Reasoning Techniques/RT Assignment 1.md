#### Task 1

Variables:
* A=AMY,  
* D=DAPHNE, 
* F=FLORA, 
* J=JOHN, 
* K=KEITH, 
* N=NICK, 
* S=SAM

Requirements:
1. AMY and DAPHNE had a disagreement in the past, and do not want to share the same office.  
2. FLORA and JOHN are best friends, and want to share the same office.  
3. KEITH talks too much. Only DAPHNE can share the office with him.  
4. DAPHNE is the supervisor of FLORA, JOHN, and NICK, and she is very strict. Thus, the tree of them don't want to share the office with her.  
5. SAM always listens to music at work and AMY and DAPHNE are bothered by it. Thus, neither of them wants him in the same office or an adjacent office.  
6. AMY annoys NICK, so NICK doesn't want to be in AMY's office.

a)
![[Screenshot 2023-11-13 at 1.46.34 PM.png|400]]

b)
![[Screenshot 2023-11-13 at 1.47.18 PM.png|200]]

Tree:
![[Screenshot 2023-11-13 at 7.26.17 PM.png]]

Because we assumed that Amy is the leader the root of our tree is a state where she is already assigned office 1. We then assign office to Sam (S) according to MRV heuristic, because we consider them in increasing order we first assign him office 3 but we need to backtrack so we proceed with office 4. Next we assign office to Keith (K), then Nick (N) both according to MRV. Suddenly we get a tie between Flora (F) and John (J) as they have equal MRV values. They both also have degree of 1 in current constraint graph so. we proceed with F. We find the solution!

---
#### Task 2

a) L, M, E, N, O, F, B, P, Q, G, R, S, H, T, U, I, C, V, W, J, X, Y, K, A

correction: Node A has a value of 7!
![[Screenshot 2023-11-13 at 2.49.09 PM.png|400]]

b)
![[Screenshot 2023-11-23 at 4.49.33 PM.png|400]]

---
#### Task 3

Tree:
![[Screenshot 2023-11-13 at 7.34.37 PM.png]]

Best way:
Timisoara $\rightarrow$ Arad $\rightarrow$ Sibiu $\rightarrow$ Rimnicu Vilcea $\rightarrow$ Pitesti $\rightarrow$ Bucharest. Even tough that was the first found path to Bucharest, at that moment the Bucharest node did not have the smallest $f$ value, so I expanded the tree further.
The numbers on top of states indicate the time when they where visited (1-13), under the states we calculate $f$, $f = g(n)+h(n)$.
