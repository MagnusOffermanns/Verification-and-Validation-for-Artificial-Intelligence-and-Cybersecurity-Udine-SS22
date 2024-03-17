# 1 Exercise 1:

Consider the automaton is this:

If we read a $a$ in $q_2$ we stop the computation.

![[exercises 20 automaton.png]]

is it equivalent to this automaton ($q_0$ is also a final state)

![[Verification 20_image_1.jpeg]]

==No it is not equivalent:==
When we read in the word $ba...$ we have a fail in the first automaton and while it is a valid state in the second.

# 2 Exercise 2:
Build the finite state automaton that recognizes the finite variant of L.

It is the same as the automaton above.
[[Finite State Automata]]

# 3 Exercise 3
Let $W$ be the language of Ex.2. Provide a characterization i.e. an [[Deterministic Finite State Automata|Automaton]] that recognizes the [[Vectorial closure]]  of $W$ i.e. $\vec{W}$

$\overrightarrow{w}=\{\alpha \in A^w: \exists^w n \quad \alpha(0,n) \in w \}$    


Could it be that it is the automaton from above again?
# 4 Exercise 4

> [!note] [[Theorem 8]]
> 1. if $V \subseteq A^*$ is regular, then $V^w$ is [[w-regular]].
> 2. If $V \subseteq A^*$ is regular and $L \subseteq A^w$ is [[w-regular]], then $V \cdot L$ is [[w-regular]].

What does $V^w$ means? A word $v \in V^w = v_0,v_1,v_2,v_3...$ and every $v_n$ is in $V$.

That means this are the infinite word obtained by concatinating the individual words of the finite word language $V$ after each other infinitely many times.

Question prove point 2:
 $V \cdot L$ is a [[Buechi automata]] meaning to accept a word it needs to go infinitely many times through a final state.

==3== cases:
1. case: 
	$a$ is not a word of $V \cdot L$ in particular it fails in V
	if a prefix of $a$ is not accepted by $V$ it will stop in the automaton of $V$ i.e. the word is not accepted.
2. case $v$ is a word accepted by $V$ but not by $L$ then if we create a automaton that has a link from all final states of $V$ to the initial state of $L$ it will get accepted by $V$ but then not accepted by $L$
3. case the word $v \cdot l$ has a prefix that is accepted by $V$ ($v$) clearing the finite state automaton, and then a postfix ($l$) that is accepted by $L$ it will be accepted by the entire automaton.

This means that one can always create a automaton 
that accepts $V \cdot L$ by connecting all final states  of $V$to the inital state of $L$.

# 5 Exercise 5
> [!note] [[Theorem 8]]
> 3. $L_1,L_2 \subseteq A^w$ are [[w-regular]], then $L_1 \cup L_2$ and $L_1 \cap L_2$ are [[w-regular]] as well.
Prove part 3 of [[Theorem 8]].

1. $L_1 \cup L_2$
Simmilar to the closure property in [[Verification 11]]. We let two automaton run at the same time. If one of them does not accept the word we stop computation
2. $L_1 \cap L_2$
Like above we let two automaton run. But we have to consider synchronicity as it is not for sure that both [[Deterministic Finite State Automata|Automata]] are passing through the final state at the same time. 
Therefore we create an automaton which final state has a exit condition of the final state of the other automaton. This means that the automaton can only leave the final state if the other automaton also is in  the final state i.e.  that the state ($(q_{f1}|?)$) which means that the first automaton is in a final state only has a connection to $(q_{f_1}|q_{f_2})$ and the same for the other automaton. This means that the state does not change until both automaton are in the final state, hereby making it possible that both of them pass through the final state at the same time (infinitely many times).

