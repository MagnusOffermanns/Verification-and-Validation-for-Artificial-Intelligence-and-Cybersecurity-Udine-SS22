> [!note] [[Corollary 4]]
> Every non-empty [[w-regular|w-regular-language]] $L$  includes at least one ultimately periodic word


==Proof:==
Let $L$ be a [[w-regular|w-regular-language]]. By [[Theorem 8]] we have that $L = \cup_{i_1}^n U_i \cdot V_i$ with $v_i,u_i \subseteq A^*$ is regular.

Since $L \neq \emptyset$  it follows that there exists $\alpha=u\cdot v_1 \cdot v_3...$

And all the $v$ have the length $i$ and therefore belong to $V_i$. $i$ is greater 0 and smaller $n$.

It immediately follows that we can create a word that is:
$$\beta=u \cdot v_1 \cdot v_1 ...= u \cdot v^w \in L$$


