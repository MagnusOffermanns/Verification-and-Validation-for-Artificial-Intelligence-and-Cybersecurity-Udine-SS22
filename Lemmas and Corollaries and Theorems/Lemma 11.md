==Shortform:==  If you can find a word $w$ for an [[Deterministic Finite State Automata|Automaton]] it has less symbols than there are states in the [[Deterministic Finite State Automata|Automaton]]

Long form:
For every [[Non Deterministic Finite State Atomata|NFA]] $\mathcal{A}$ the [[Language]] $L(\mathcal{A}) \neq \emptyset$ if and only if there exists a word $w$ which is an element of its alphabet $A$ is element of the language $L(\mathcal{A})$ and has less symbols than there are states in the [[Deterministic Finite State Automata|Automaton]]i.e. $|w|<|states|$

This is usefull when we want to find a accepted word. We just need to check all paths through our [[Deterministic Finite State Automata|Automaton]] with length smaller or equal $n-1$