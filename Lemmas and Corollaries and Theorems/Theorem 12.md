> [!note] [[Theorem 12]]
> Let $\sim$ be a [[Congruence]] and $L \subseteq A^w$ be a [[w-regular|w-language]]. If $\sim$ saturates $L$, then $\sim$ also saturates $\overline{L}$.

==Proof by contradiction:==
Let us assume that $\sim$ does not saturate $\overline{L}$. This implies there exists two [[Equivalence class]]es $u,v$ such that $u \cdot v^w \cap \overline{L} \not  = \emptyset$ but there is an element that is not part of $\overline{L}$ i.e. $u \cdot v^w \not \subseteq \overline{L}$. By $u \cdot v^w \not \subseteq \overline{L}$ it follows that there exists a [[omega-words|w-word]] $\alpha$ such that exists $\alpha \in u \cdot v^w$ and $\alpha \in L$. Since $\sim$ [[Saturation|saturate]]s $L$,  if one word $\alpha$ is in $L$ all words need to be in L. Therefore from $\alpha \in u \cdot v^w \cap L$ , it follows that $u \cdot v^w \subseteq L$ is a contradiction




