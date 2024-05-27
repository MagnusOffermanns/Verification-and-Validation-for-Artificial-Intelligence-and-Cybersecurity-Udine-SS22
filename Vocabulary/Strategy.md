---
aliases:
  - winning strategy
  - Determined games
  - Finite state Strategy
  - positional strategy
---
# 1 Strategy
- A [Strategy](Strategy.md) for a player is a mapping $f : Q^+ \to Q$ such that, given the history of the game up a certain state (under his/her control), specifies his/her behavior at the next step.

# 2 Winning strategy
 A strategy $f$ for player $B$ from $q$ is a [winning strategy](Strategy.md) if each play from $q$, played according to f , is won by player B.
## 2.1 Winning region
 $W_B := \{q \in Q | B \text{ wins starting from } q\}$ is said the winning region of $B$ (the same for $A$) from the set of states from where $B$ winns. 
- Obviously, $W_A \cap W_B = \emptyset$.
# 3 Determined games

If $W_A \bigcup W_B=Q$   we say that the game is a determined game. This means that depending on the start position it is already determined who will win.

# 4 Finite state Strategy


In easy words it means that **we can build a finite state [Mealy automaton](Mealy%20automaton.md) that tells us how to win the game.**

Formally, $f$ is a finite state strategy if it can be computed by a Mealy automaton of the form $S = (S, Q, Q, s_0 , \delta, \tau )$ , where $S$ is a finite set of states, $Q$ is both the input and output alphabet, $s_0 \in S$ is the initial state, $\delta : S \times Q \to S$, and $\tau : S \times Q_A \to Q$, for $A$, and $\tau : S \times Q_B → Q$, for $B$.
$\delta$ is the transitions function telling us how we move in the [Mealy automaton](Mealy%20automaton.md).
$\tau$ are the transition functions defining to which state we need to go depending on the current state of the game $Q_A$ or $Q_B$ and the state of the [Mealy automaton](Mealy%20automaton.md) $S$.


# 5 Positional strategy
A strategy is positional if the value of $f(q_1,\dots,q_k)$ only depends **on the current state $q_k$**. A positional strategy for $B$ is a mapping $f: Q_B \to Q$ (similarly for $A$)

A positional strategy always the same one move, leading to victory in every, for every state.

When looking at this automaton, we need to win by always taking the same edge every time we come into one of the edges. Meaning that in this case, we would only go infinitely many times through two of the nodes. (either $1,2$ or $2,3$)
![](Strategy_image_1.png)

After [Theorem 26](Theorem%2026.md) [Reachability Games](Muller%20Game.md) have a winning [positional strategy](Strategy.md).