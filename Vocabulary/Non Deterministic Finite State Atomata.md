---
aliases: NFA
---
# 1 [Non Deterministic Finite State Atomata](Non%20Deterministic%20Finite%20State%20Atomata.md)
An [[Non Deterministic Finite State Atomata|NFA]] $\mathcal{A}$ is  a tuple ($Q,A,\Delta,q_0,F$) where $Q,A,q_0$ and $F$ are defined as in [[Deterministic Finite State Automata|DFA]] except for the transition function $\delta$ where:
$$\delta: Q \times A \rightarrow 2^Q$$
That means that from one state $q$ one can reach more than one state when it gets a symbol as input. Depending on a random variable for example)

# 2 NFA with epsilon move

>[!note] Definition: [[NFA with epsilon-move]]
> We have an [[Deterministic Finite State Automata|Automaton]] $(Q,A,\Delta,q_0,F)$ where $Q,A,q_0$ and $F$ have definitions equla to the normal [[Non Deterministic Finite State Atomata|NFA]]. 
> The only difference is $\Delta$
> $\Delta: Q \times (A \cup\{\epsilon\}) \rightarrow 2^Q$
> 
> This means that independent of the state one is in it is always possible to read the empty word $\epsilon$ as input. This is simmilar to a idle move.
> 
> How do we define $\hat{\Delta}$ the transition function accepting words?
> 
> $\hat{\Delta}(q,\epsilon)=\epsilon\text{-closure}(q)$
> 
