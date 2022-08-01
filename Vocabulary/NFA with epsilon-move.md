We have an [[Deterministic Finite State Automata|Automaton]] $(Q,A,\Delta,q_0,F)$ where $Q,A,q_0$ and $F$ have definitions equal to the normal [[Non Deterministic Finite State Atomata|NFA]]. 
The only difference is $\Delta$
$\Delta: Q \times (A \cup\{\epsilon\}) \rightarrow 2^Q$ 

This means that independent of the state one is in it is always possible to read the empty word $\epsilon$ as input. This is simmilar to a idle move.

How do we define $\hat{\Delta}$ the transition function accepting words?

$\hat{\Delta}(q,\epsilon)=\epsilon\text{-closure}(q)$

How do we generalize it to entire words $w$ preceded by a symbol $a$?
$\hat{\Delta}(q,wa)=\epsilon\text{-closure}(\bigcup\limits_{p \in \hat{\Delta}(q,w)}\Delta (p,a)$

What does this mean? It is the $\epsilon$-closure of all states that one can reach by first applying first  the word $w$ followed by  a symbol $a$. For an example see [[Verification 10]].

The acceptance condition is the same as with normal [[Non Deterministic Finite State Atomata|NFA]]s