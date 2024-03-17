We have the algorithm [[P-SAT]] to check the [Satisfiability](Satisfiability.md) of a formula $\varphi$ over a program (to check whether a finite-state program $P$ has a
computation which satisfies a temporal formula $\varphi$)

What are the [P-SAT](P-SAT.md) steps for the program $P$ and the formula $\varphi$:
1. Construct the state-transition graph $G_p$
2. Construct the pruned [Tableaux](Tableaux.md) $T_\varphi$
3. Construct the [behavior graph](behavior%20graph.md) $B_{(P,\varphi)}$
4. Decompose $B_{(P,\varphi)}$ into [MSCS](VV%20Strongly%20connected%20subgraph.md) $S_1,\dots,S_t$
5. For each of the [MSCS](VV%20Strongly%20connected%20subgraph.md) apply the algorithm $ADEQUATE-SUB$ to identify [Adequate subgraphs](Adequate%20subgraphs.md)

(Introduced in [[Verification 33]])