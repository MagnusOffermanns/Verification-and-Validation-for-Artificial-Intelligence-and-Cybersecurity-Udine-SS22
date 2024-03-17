---
aliases:
  - Weak muller game
  - Reachability Games
  - w
---
# 1 Arena
Is deducted from a [Muller Automata](Muller%20Automata.md).
The following [Muller Automata](Muller%20Automata.md) becomes the following arena:

Automata:
![](Verification%2043_image_7.png)

Arena:
![](Verification%2043_image_11.png)

# 2 Winning condition
- [Muller Game](Muller%20Game.md)
	 Muller games: the winning condition is a collection of sets of states $F ⊆ 2^Q$ such that $B$ wins $\rho$ if and only if $Inf(ρ) ∈ F$. That is simmilar to the original [Muller Automata](Muller%20Automata.md) acceptance condition
- [Weak muller game](Muller%20Game.md)s
	There exists a weak version of the winning condition of Muller games (Staiger-Wagner condition), according to which $B$ wins the play $ρ$ if and only if $Occ(ρ) ∈ F$, where $Occ(\rho) = {q \in Q : \exists i(\rho(i) = q})$. That means that we do not have to traverse a state $p$ infinitely many times, but $p$ only needs to be traversed once.
- [Reachability Games](Muller%20Game.md)
	We define a set of winning sates $F \in Q$. $B$ wins the play $\rho$ if some state in the play belongs to $F$.