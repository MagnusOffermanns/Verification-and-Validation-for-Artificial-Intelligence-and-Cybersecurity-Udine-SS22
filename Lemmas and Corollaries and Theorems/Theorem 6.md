---
aliases: Myhill-Nerode Theorem, Myhill-Nerode equivalence
---

Let L be a Language over the Alpabet $A^\star$ i.e.: $L \subseteq A^\star$. $L$ is ==any== Language.
Then the following conditions are equivalent:
1.  $L$ is [[Regular Languages|regular]]
2.  There is a [[Equivalence problem|equivalence relation]] $\approx$ over words element of $A^\star$ that is [[finite index]] (i.e. has a finite amount of equivalence classes) and is [[right invariant]] such that $L$ us a union of [[Equivalence problem| equivalence classes]] ($\approx-classes$) .
e.g.
$$L=[u_1]_\approx \cup [u_2]_\approx \cup [u_3]_\approx ... $$
($[u_1]_\approx$ is the class of all words that are equivalent to the word $u_1$)
3. Some particular equivalence $\approx_l$ is [[finite index]]. This equivalence is also called [[Theorem 6|Myhill-Nerode equivalence]].
 > $\approx_L$ is defined as:
 > $u \approx_L v \quad \iff  \quad \forall t \in A^\star \hspace{0.5em} ( u \cdot t \in L \iff v \cdot t \in L)$


# 1 For functions:
The [[Theorem 6|Myhill-Nerode equivalence]] also exists for functions:
> [!note] for functions:
> $u \approx_{f_0} v \text { if } \forall t \in \sum^* \quad f_0(u t)-f_0(u)=f_0(v t)-f_0(v)$

What are ==properties== of the [[Theorem 6|Myhill-Nerode equivalence]] for functions?
- It is right invariant
- it has finite index if and only $\iff$ if  $f$ is computed by a [[Sequential Transducer]].