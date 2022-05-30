 ==Deterministic:==
 Defines how a word $w$ needs to be formed so that  a [[Deterministic Finite State Automata|Automata]] $\mathcal{A}$ (starting from a initial state $q_0$) after processing ends in a state which is part of the set of final states $F$. 
i.e $\hat{\delta}(q_0,w) \in F$

==Non-Derterministic:==
A word $w$ is accepted by a [[Non Deterministic Finite State Atomata|NFA]] $\mathcal{A}$ if (and only if) $\hat{\delta}(q_0,w) \bigcap F \neq \emptyset$. 

This means that when a word is applied to an [[Deterministic Finite State Automata|Automata]] there needs to be a chance for it to finish in a state which is part of the final states. i.e. one of the states in the set of all states that the [[Deterministic Finite State Automata|Automata]] can be in after applying a word needs to be in the set of final states $F$.