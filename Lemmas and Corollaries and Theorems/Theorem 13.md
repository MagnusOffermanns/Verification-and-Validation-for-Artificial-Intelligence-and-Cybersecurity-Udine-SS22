> [!note] [[Theorem 13]]
> If $L \subseteq A^w$ is [[w-regular]], then $\overline(L)(= A^w-L)$ is [[w-regular]] as well. Moreover from a [[Buechi automata|Buechi-automaton]] for $L$ we can build a [[Buechi automata|Buechi-automaton]] for $\overline{L}$

==proof [[Theorem 13]]==

Let $\mathcal{A}$ be a [[Buechi automata|Buechi-automaton]] such that $L(\mathcal{A})=L$.

What do we already know?
1. $\approx_a$ is a [[Congruence]] of [[finite index]] that [[Saturation|saturate]]s $L$ and $\overline{L}$.

By [[Corollary 6]] it follows that:
$$\overline{L} = \cup u \cdot v^w$$
where $u,v$  are $\approx_A$ classes such that $u \cdot v^w \cap \overline{L} \not = \emptyset$
Since $u,v$ are regular languages i.e. we can build [[Finite State Automata]] for both of them, and [[w-regular]] languages are closed under [[w-closure]], [[Concatenation]] and [[Union]] we can conclude that $\overline{L}$ is [[w-regular]].

What does this mean:
1. We can not leave [[w-regular]] languages when applying the union $\cup$
2. We can not leave [[w-regular]] languages when applying concatenation ($u \cdot v$)
3. We can not leave [[w-regular]] languages when applying the $w$ operator i.e. $v^w$

As we can create $\overline{L}$ using this operators and [[Finite State Automata]] we can be sure that also $\overline{L}$ is a [[w-regular]].