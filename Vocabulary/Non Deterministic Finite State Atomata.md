---
aliases: NFA
---
An [[NFA]] $\mathcal{A}$ is  a tuple ($Q,A,\Delta,q_0,F$) where $Q,A,q_0$ and $F$ are defined as in [[Deterministic Finite State Automata|DFA]] except for the transition function $\delta$ where:
$$\delta: Q \times A \rightarrow 2^Q$$
That means that from one state $q$ one can reach more than one state when it gets a symbol as input. Depending on a random variable for example)