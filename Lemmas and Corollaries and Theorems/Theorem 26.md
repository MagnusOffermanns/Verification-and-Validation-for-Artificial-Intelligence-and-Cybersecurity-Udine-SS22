>[!Note] [[Theorem 26]]
>A [Reachability Games](Muller%20Game.md) $(G, F)$, with $G = (Q, Q_A , E)$ and $F \subseteq Q$, is determined and both the winning regions $W_A$ and $W_B$ for players $A$ and $B$, respectively, and the corresponding positional winning strategies are computable.



>[!Note] Proof
> For $i = 0, 1,\dots$, compute the vertices starting from which player $B$ can force a visit in $F$ in at most $i$ moves ($i^{th}$ attractor $Attr^i_B (F)$).
> 
> When do we add a state to the set of $Attr_B$? If it is a state under the control of $B$ there needs to be one edge to a state that is already part of $Attr_B$. If the state is under control of $A$ all ($\forall$) edges need to go to a state that is already part of $Attr_B$.
> 
>The sequence $Attr^0_B (F)(= F) \subseteq Attr^1_B(F) \subseteq Attr^2_B(F) \dots$ becomes It stationary can be easily for some proved index that $k ≤ |Q|$. We define $Attr_B=\bigcup^{|Q|}_{i=0}Attr^i_B(F)$.
> It can easily be prooven that $W_B=Attr_B(F)$.


