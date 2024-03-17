This is the second part of the video Verification 26, the first part is in the note [[Verification 25]].

# 1 [[Determinization]]
[[Buechi automata]] are not deterministic, we know that they are more complex to handle than deterministic automata, but why do we choose to use the [[Non deterministic]] properties? Because a deterministic [[Buechi automata]] would be ==less expressive==.

## 1.1 [[Buechi automata|Deterministic Buechi Automata]] ([[Buechi automata|DBA]])

$$\mathcal{A}=(Q,A,\delta,q_0,F)$$
where $Q,A,q_o$ and $F$ are defined as for Non-deterministic [[Buechi automata]]. $\delta$ is defined as consuming one symbol and going from one state to another i.e. $\delta : Q\times A \rightarrow Q$ .

The computation of $\sigma$ of $\mathcal{A}$ is successful on the input  $w-word$ $\alpha$  if the number of states that we pass through infinitely many times contains one set that is part of the final states $F$ i.e. $In(\delta) \cap F \not = \emptyset$ .

Acceptance and language defined by $\mathcal{A}$ are as for non deterministic [[Buechi automata]] ([[Buechi automata|NBA]]). There is only one computation on a word is possible as it is non deterministic.

Exercise: Prove that [[Buechi automata|DBA]]s are closed under union and intersection.

Hints: The prove of intersection and union is similar to the prove of the same features of [[Buechi automata|NBA]]. In the [[Buechi automata|NBA]] prove we exploit non determinism here we can not.


> [!note] [[Theorem 17]]
> A Language $L \subseteq A^\omega$ (a language of infinite words )is recognized by a [[Buechi automata|DBA]] if and only if ($\iff$) it can be written as the [[Vectorial closure]]  of a language $L$ i.e. $L=\vec \omega$ for some regular language $\omega \subseteq A^*$

## 1.2 ==Prove==
Let $\mathcal{A}=(Q,A,\delta,q_0,F)$ be a [[Buechi automata|DBA]] and let $\mathcal{A'}=(Q,A,\delta,q_0,F)$ be the corresponding [[Deterministic Finite State Automata|DFA]]. Let $w \subseteq A^*$ be the language recognized by $\mathcal{A'}$  i.e. $L(\mathcal{A'})$.

We prove now that $L(\mathcal{A}=\vec w)$

By definition of acceptance condition of [[Buechi automata]] and the deterministic nature of the automaton $\mathcal{A}$, we have that $\mathcal{A}$ if and only if the computation on $\alpha$ is successful that is $In(\delta) \cup F \not = \emptyset$. 

![[VV26_1.jpeg]]

It follows that there are infinitely many prefixes that belong to $w$ and thus we can conclude that the $\alpha \in \vec w$ i.e. $\alpha$ is part of the  [[Vectorial closure]] of $w$.

Lets assume now that $\alpha \in \vec w$. For all prefixes of $\alpha$ belonging to $w=L(\mathcal{A'})$ the successful computation of $\mathcal{A'}$ of them can be viewed as a prefix of the unique computation of $\mathcal{A}$ on $\alpha$.

![[VV26_2.jpeg]]

Since $In(\delta) \cap F \not = \emptyset$. It follows that $\alpha \in L(\mathcal{A})$







