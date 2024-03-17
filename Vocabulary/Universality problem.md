---
aliases: universal
---
- Is [[logical equivalence|logically equivalent]] to the [[Validity]] of a Formula in [[FO - First order logic|FO]].

In this problem we check weather the set of accepted words  is equal to the entire [[Alphabet]]  of the [[Deterministic Finite State Automata|Automaton]] i.e.
$$L(\mathcal{A}) = A$$

==input:== [[Non Deterministic Finite State Atomata|NFA]] $\mathcal{A}$  over the Alphabet $A$
==output:== Yes if the [[Deterministic Finite State Automata|Automaton]] accepts every word of the alphabet

How do we solve such a problem similar to the [[Validity]] problem in [[FO - First order logic|FO]]. We form the [[Complementation|complement]] of the Automaton. If the [[Complementation|complemented]] Automaton does not exist we know that the original [[Deterministic Finite State Automata|Automaton]] is [[Universality problem]]