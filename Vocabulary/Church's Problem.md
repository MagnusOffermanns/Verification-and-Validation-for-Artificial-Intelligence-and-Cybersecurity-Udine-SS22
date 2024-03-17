
Given an [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)-formula φ(X, Y), build a Mealy automaton M, with input alphabet $\Sigma = \{0, 1\}$ and output alphabet $\Gamma = \{0, 1\}$, such that, for every input sequence $α ∈ \{0, 1\}^\omega$ ,the [Mealy automaton](Mealy%20automaton.md) $\mathbb{M}$ generates an output sequence $β ∈ {0, 1}^\omega$ such that $(w,1)\models \varphi[P_\alpha,P_\beta]$ (or it answers that such an automaton does not exist).

It can be easily generalized to an input alphabet $\Sigma = \{0, 1\}^{m_1}$ and/or to an output alphabet $\Gamma = \{0, 1\}^{m_2}$.
A finite state winning strategy for an infinite game: according to a game-theoretic interpretation, a [Mealy automaton](Mealy%20automaton.md) can be viewed as the definition of a winning strategy for player $B/β (Bob)$ that replies to the moves of player $A/α (Alice)$.

Summarizing:
1. Is it possible to satisfy the specification?
2. Lets synthesize the automaton
