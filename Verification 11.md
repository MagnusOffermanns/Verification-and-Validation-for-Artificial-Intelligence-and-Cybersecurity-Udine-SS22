In the first part the second part of the proof of[[Theorem 4]]  is discussed to not have a cut I completed the proof in [[Verification 10]].

==Starting with 11 b==

# 1 [[Theorem 5]]
> [!note] Theorem 5 the [[Theorem 5|Closure Property]]
> [[Regular Languages]] are closed under [[Boolean Operations]] ($\cup,\cap,\neg$), [[Concatenation]] and the [[Kleene-closure|Kleene star]]. Moreover the construction of the [[Deterministic Finite State Automata|Automaton]] that recognizes the language obtained from the application of the operation is [[effektive]].

What does it mean: If you have two regular language and you apply one of the operators the result is still a regular language.

## 1.1 Proof of [[Theorem 5]] 
We already proved it already for $\cup,\cdot,\star$ in the proof of [[Theorem 4]].

To complete the proof we need to consider the two remaining operations $\cap$ and negation $\neg$. Which means that given an Automaton $\mathcal{A}$ for $L \leq A^*$ (i.e $L(A)=L$ in words: The language that is accepted by the automaton $\mathcal{A}$ is $L$) we need to define a automaton that represents $\neg L$.

Let:
 $\mathcal{A}_1=(Q,A,\delta,q_0,F)$ be a [[Deterministic Finite State Automata|DFA]] for $L$
 
 A [[Deterministic Finite State Automata|DFA]] $\mathcal{A}'$ for  the complement of $L$ i.e. $\neg L$:
 
 $\mathcal{A}=(Q,A,\delta,q_0,Q-F)$
 
 We choose to use [[Deterministic Finite State Automata|DFA]]s because of its deterministic properties -> complicated explanation not covered here.
 
 - Why $Q-F$?
 > We say that all words are accepted that do not end in one of the final states of $\mathcal{A}$.
 
 - Why do we need to alter the transition function?
 > There are two ways that words do not get accepted:
 > 1. The entire word is read, but in the end we do not end up in a final state.
 > 2. The other case occurs if the word is read and we end up in a state from which there is ==no exiting== transition for the next symbol. i.e. the automaton does not know what to do with the next symbol. We call such an automaton  [[Deterministic Finite State Automata#1 Completeness|incomplete]].
 > The problem is now that the new automaton will do also fail to read the word, if there is no transition function out of the symbol. Therefore we need to define a transition function $\delta_{new}$for all states for all symbols not originally defined in $\delta$. Therefore we create a final  state which one can transition to if a symbol does not have a transition function and then stays in this state till the word is read in. Then the word is accepted. Of course $q_{failure} \notin F$ See the image below:
 
 ```mermaid
graph LR

title[<u>DFA with failure state</u>]
start --> q1
q1((q1))--A-->q2((q2))--A-a -->dot((...))
q2-- a -->qfail((q_fail))
qfail--A-->qfail
final-->qfail
```
==Learning:== Not every complement [[Deterministic Finite State Automata|Automaton]] needs a failure state. For instance if it is [[Deterministic Finite State Automata#1 Completeness|complete]] one is not needed. But we can make every complement [[Deterministic Finite State Automata|Automaton]] [[Deterministic Finite State Automata#1 Completeness|complete]] if we add a failure state

With that we know that also the complement of an [[Deterministic Finite State Automata|Automaton]] is a automaton.

### 1.1.1 Closure under [[Intersection]] $\cup$
Closure for [[Intersection]] follows from the fact that [[Intersection]] can be defined using [[Union]] and [[Complementation]].

Still we will show how it works:

We have two languages $L1$ and $L2$ we want to find an [[Deterministic Finite State Automata|Automaton]] for $L1 \cap L2$.

The [[Deterministic Finite State Automata|DFA]]s for $L1$ and $L2$ are:
$$\mathcal{A}_1=(Q_1,A,\delta_1,q_1,F_1)$$
$$\mathcal{A}_2=(Q_2,A,\delta_2,q_2,F_2)$$

How can we build an Automaton $\mathcal{A}_2$ for $L_1 \cap L_2$?

$$A=(Q_1 \times Q_2,A,\delta,(q_1,q_2),F_1 \times F2)$$

1. $Q_1 \times Q_2$ is the [[Kartesian product]] of $Q_1$ and $Q_2$. This implies that we pairs of states (see 3. point) and that we get a state for each combination of the individual states of $Q_1$ and $Q_2$.
2. The Alphabet stays the same
3. $\delta((q_x,q_y),a)=(\delta_1(q_x,a),\delta_2(q_y,a))$. 
> One decisive thing here is that we kind of have two [[Deterministic Finite State Automata|Automata]] at the same time. One being $A_1$ and the other being $A_2$.  For the Automaton to accept the word both [[Deterministic Finite State Automata|Automata]] need to finish successfully.

 ```mermaid
graph LR
title[<u>DFA with two Automata at the same time</u>]
start--> qy
start-->qx
qy--a-->qy+1
qx--a-->qx+1
qy+1-->...1((...))
qx+1-->...2((...))
```
 [[Exercises session 11]] 
 ==How can we make that the newly constructed automata from an intersection works for mixed automata i.e. one [[Deterministic Finite State Automata|Automaton]]  being finite. The other one infinite.==

==probable solution== If the finite state accepts a word it goes into a final state similar to the in [[Verification 11]] introduced failure state. There it stays infinitely for each word of the alphabet $A$. As it then stays in this final state forever it counts as successful word read.

4. $(q_1,q_2)$ the starting state are the pair of the starting state of $A_1$ and $A_2$ 
5. The final states  are $F_1 \times F2$ again a pair for every combination of final states of $A_1$ and $A_2$.

Now Reusing the proofs for the [[Boolean Operations]] and the [[Concatenation]] we did for the proof of [[Theorem 4]] we know have shown [[Theorem 5]] i.e. that [[Regular Languages]] are closed under the noted operations.