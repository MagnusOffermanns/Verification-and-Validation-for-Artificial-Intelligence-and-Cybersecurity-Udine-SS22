
> [!note] [[Theorem 17]]
> A Language $L \subseteq A^\omega$ (a language of infinite words )is recognized by a [[Buechi automata|DBA]] if and only if ($\iff$) it can be written as the [[Vectorial closure]]  of a language $L$ i.e. $L=\vec \omega$ for some regular language $\omega \subseteq A^*$

## 0.1 ==Prove==

Let $\mathcal{A}=(Q,A,\delta,q_0,F)$ be a [[Buechi automata|DBA]] and let $\mathcal{A'}=(Q,A,\delta,q_0,F)$ be the corresponding [[Deterministic Finite State Automata|DFA]]. Let $w \subseteq A^*$ be the language recognized by $\mathcal{A'}$  i.e. $L(\mathcal{A'})$.

We prove now that $L(\mathcal{A}=\vec w)$

By definition of acceptance condition of [[Buechi automata]] and the deterministic nature of the automaton $\mathcal{A}$, we have that $\mathcal{A}$ if and only if the computation on $\alpha$ is successful that is $In(\delta) \cup F \not = \emptyset$. 

![[VV26_1.jpeg]]

It follows that there are infinitely many prefixes that belong to $w$ and thus we can conclude that the $\alpha \in \vec w$ i.e. $\alpha$ is part of the  [[Vectorial closure]] of $w$.

Lets assume now that $\alpha \in \vec w$. For all prefixes of $\alpha$ belonging to $w=L(\mathcal{A'})$ the sucessfull computation of $\mathcal{A'}$ of them can be viewed as a prefix of the unique computation of $\mathcal{A}$ on $\alpha$

![[VV26_2.jpeg]]

Since $In(\delta) \cap F \not = \emptyset$. It follows that $\alpha \in L(\mathcal{A})$


