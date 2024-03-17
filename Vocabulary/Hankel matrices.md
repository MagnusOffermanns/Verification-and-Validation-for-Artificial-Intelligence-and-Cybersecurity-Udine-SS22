infinite matrix representing a Language $L_0$. it is highly redundant.


![[Hankel-Matrix 1.png]]

Works also for [[Non Deterministic Finite State Atomata|NFA]] instead of the 1's or 0's one puts in probabilities.

One row represents one equivalence of the [[Theorem 6|Myhill-Nerode equivalence]]. When rows are simmilar the [[Word|words]] are in the same equivalence class. ==How many rows do we maximally have?== The number of states of the minimal [[Deterministic Finite State Automata|Automaton]] .

A column represents a test word (a word from our set $T$).

And a sub row represents the [[Equivalence class]] using only the included test words i.e. the [[Equivalence class]] under $=_{L_{0}T}$