# 1 What is the difference between [[Accessibility property]] and [[Mutual exclusion Problem]] and why does [[Compassion]] not play a role when proving the latter.



# 2 in [Verification 37](Verification%2037.md)
How does this work with the synax of $z$ and how do we find the formula that we use to converge to the possible solutions.

$E(F(f_1))=\mu z.f_1 \lor E(X(z))$

# 3 in verfication [Verification 43](Verification%2043.md)
How do we convert a [Muller Automata](Muller%20Automata.md) to a [Muller Game](Muller%20Game.md)

![](Questions_image_1.png)

# 4 What is the difference between [Weak muller game](Muller%20Game.md) and [Reachability Games](Muller%20Game.md)
[Verification 43](Verification%2043.md)

The two winning conditions look the same to me...

- [Muller Game](Muller%20Game.md)s: the winning condition is a collection of sets of states $F ⊆ 2^Q$ such that $B$ wins $\rho$ if and only if $Inf(ρ) ∈ F$. That is simmilar to the original [Muller Automata](Muller%20Automata.md) acceptance condition
- [Weak muller game](Muller%20Game.md)s
	There exists a weak version of the winning condition of Muller games (Staiger-Wagner condition), according to which $B$ wins the play $ρ$ if and only if $Occ(ρ) ∈ F$, where $Occ(\rho) = {q \in Q : \exists i(\rho(i) = q})$. That means that we do not have to traverse a state $p$ infinitely many times, but $p$ only needs to be traversed once.
- [Reachability Games](Muller%20Game.md)
	We define a set of winning sates $F \in Q$. $B$ wins the play $\rho$ if some state in the play belongs to $F$.

## 4.1 What is the solution of a Game?
The [[solution of a game]] $(G,W)$ and $G=\{Q,Q_A,E\}$ and $W$ finitely describable, consists of two steps:
1. to establish for each $q \in Q$ if $q \in W_A$ or $q\in W_B$


# 5 Can a fluent be both [inertial](fluents.md) and [non-inertial](fluents.md)

That means variables can be changed by actions, as well as by the environment and not only by one of the two.

see [Verification 46](Verification%2046.md)
