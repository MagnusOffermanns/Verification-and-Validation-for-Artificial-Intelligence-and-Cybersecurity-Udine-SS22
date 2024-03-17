[[T-Minimal]] and [[T-complete]] are repeated.

# 1 The learning algorithm to teach a [[Deterministic Finite State Automata|Automaton]]

$T$ = test set -> is used to test if the automaton works.

We start start with empty sets $T$ and $S$ i.e. $\{\epsilon \}$.

The first goal is to make the set $S$ [[T-complete]]

Therefore we go into a while loop. 
We look for a $s$ and a word $a$ that does not have a equivalent in the set $S$. Then we add the concatenated $s$ and $a$ i.e. $s \cdot a$.

We do not violate [[T-Minimal]] property because we only add $sa$ if there is no $s'$ that is equivalent to $sa$. How often do we do this? As $S$ represents the [[Equivalence class]]es of a equivalence that is coarser than the [[Theorem 6|Myhill-Nerode equivalence]] the most number is the [[Cardinality]] of the [[Theorem 6|Myhill-Nerode equivalence]]-1.

Now that S is [[T-Minimal]] and [[T-complete]] we create a [[Deterministic Finite State Automata|Automaton]] $A$ where $S$ is the set of states, the initial state $\epsilon$, the transition function defined by the equivalence of $\approx_{L_{0}T}$ i.e jumping from one equivalence class to another (see [[Verification 13|V&V13]]). The final states are all strings that belong to the language.

The next step is to launch the equivalence querry to ask the teacher if my [[Deterministic Finite State Automata|Automaton]] accepts the secret language.

If it does not accept the language we get a counter example. 
We extend then the set $T$ with the counter example $w$ ad all suffixes of $w$. So the word and all substrings.

If we add the counterexample $w$ S will become [[T-complete|T-incomplete]]. This is prooved in this session of [[Verification 14|V&V]].

==Special features of the learned [[Deterministic Finite State Automata|DFA]]==
1. It is optimal. It has as little states as possible
2. It has for every state one transition for every letter that can occur.

 ```mermaid
graph LR
title[<u>Possible learned automaton</u>]
start --> epsilon
final --> epsilon
epsilon--a-->a(("a"))
a --b-->epsilon
a --a--> b
epsilon --b-->b
```
 ```mermaid
graph LR
title[<u>impossible to learn automaton</u>]
start --> epsilon
final --> epsilon
epsilon--a-->a(("a"))
a --b-->epsilon
```

The entire algorithm can be seen in this screen shot and is [[P-Time|polynomial time]].

![[learner_strategy.png]]


Now we do a example from 30:00 on to the pause.

---
Break

---

Now we will prove that $S$ will become [[T-complete|T-incomplete]] when adding the counterexample. It is a prove by contradiction

![[proove_summary_s-t-incomlete.png|400]]i


## 1.1 [[Hankel matrices]]

infinite matrix representing a Language $L_0$. it is highly redundant.


![[Hankel-Matrix 1.png]]


Works also for [[Non Deterministic Finite State Atomata|NFA]] instead of the 1's or 0's one puts in probabilities.

One row represents one equivalence of the [[Theorem 6|Myhill-Nerode equivalence]]. When rows are simmilar the [[Word|words]] are in the same equivalence class. How many rows do we maximally have? The number of states of the minimal [[Deterministic Finite State Automata|Automaton]] .

A column represents a test word (a word from our set $T$). 

And a sub row represents the [[Equivalence class]] using only the included test words i.e. the [[Equivalence class]] under $=_{L_{0}T}$.