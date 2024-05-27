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
![](Muller%20Game_image_1.png)

Arena:
![](Muller%20Game_image_2.png)

# 2 Winning condition
- [Muller Game](Muller%20Game.md)
	 Muller games: the winning condition is a collection of sets of states $F ⊆ 2^Q$ such that $B$ wins $\rho$ if and only if $Inf(ρ) ∈ F$. That is simmilar to the original [Muller Automata](Muller%20Automata.md) acceptance condition
- [Weak muller game](Muller%20Game.md)s
	There exists a weak version of the winning condition of Muller games (Staiger-Wagner condition), according to which $B$ wins the play $ρ$ if and only if $Occ(ρ) ∈ F$, where $Occ(\rho) = {q \in Q : \exists i(\rho(i) = q})$. That means that $F$  has to be a subset of the set which contains all states that we traverse during the game.
- [Reachability Games](Muller%20Game.md)
	We define a set of winning sates $F \in Q$. $B$ wins the play $\rho$ if one of the states we traverse is part of $F$

>[!Note] Difference [Reachability Games](Muller%20Game.md) games and [Weak muller game](Muller%20Game.md)s
>If we have a set of sets of final states $F=\{\{a_0,a_1}\\}$ and the $Occ(p)$ the set of states that we encounter is  $Occ(p)=\{a_0\}$ we would win in the [Reachability Games](Muller%20Game.md) as $Occ(p) \subseteq \{a_0,a_1\}$. But at the [Weak muller game](Muller%20Game.md) we would loose as the set $Occ(p)=\{a_1\}$ is not contained in the set of sets $F$. On the other side if we would traverse $a_0$ and $a_1$ we would also win the reachability game. 
>
>The [Muller Game](Muller%20Game.md) adds lastly that we need to go through one of the winning sets infinitely many times, which is even more strict.