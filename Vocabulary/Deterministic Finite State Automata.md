---
aliases: DFA, Automata, Automaton
---
A [[Deterministic Finite State Automata|DFA]] $\mathcal{A}$ is a tuple $(Q,A,\delta,q_0,F)$ where
- $Q$ is a finite set of states
- $A$ is a finite set of Symbols i.e. [[Alphabet]]
- $\delta$ is a [[Transition function]]  $\delta: Q \times A \rightarrow Q$
- $q_0$ is the initial state and is $q_0 \in Q$ 
- $F$ is a subset of $Q$ i.e $F \subseteq Q$ containing all finite states

# 1 Completeness
A [[Deterministic Finite State Automata|DFA]] is complete if it has a at least one exiting transition from every state for each symbol.