---
aliases: Ehrenfeucht-Fraise Games 
---
==Players:==
- <mark style="background: #014E11F2;">Duplicator</mark> :
> Goal: Wants to prove that $S'$ and $S$ are [[n-equivalence|n-equivalent]]. 
- <mark style="background: #FF5582A6;">Spoiler</mark> :
> Goal: Want to disprove that $S'$ and $S$ are [[n-equivalence|n-equivalent]]



==Arena:==
The arena is a graph. The nodes of the graph are tuples $(u_1,...,u_i,v_1,...,v_i)$ that are chosen from the universe $u_x \in U^S$ and $v_x \in U^{S'}$

One plays __n__ rounds.
At the start there are two empty sets $S|\{\}$ and $S'|\{\}$ who will contain chosen elements of the Spoiler and the Duplicator.

==one round:==
<mark style="background: #FF5582A6;">Spoiler</mark> begins: and chooses an element $u_i$ from the universe $U^S$ or a element $v_i$ from the universe $U^{S'}$ and adds it either to $S|\{\}$ or $S'|\{\}$.

<mark style="background: #014E11F2;">Duplicator</mark> responds: and chooses and element $v_i$ from $U^{S'}$ if <mark style="background: #FF5582A6;">Spoiler</mark> has chosen a element $u_i$ from $U^S$ or by choosing a element $u_i$ from $U^S$ if <mark style="background: #FF5582A6;">Spoiler</mark> has chosen a $v_i$ from $U^{S'}$ and adds it to the sets.

==Who wins?==
The <mark style="background: #014E11F2;">duplicator</mark> wins if after n turns  the two sets (now containing the chosen elements of $u_x$ and $v_x$) $S|\{u_1,...,u_n\}$ and $S'|\{v_1,...,v_i\}$ are [[isomorphic]]
