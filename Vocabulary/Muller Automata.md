---
aliases:
  - DMA
  - NMA
  - Non-deterministic Muller Automata
  - Deterministic Muller Automata
---
> [!Definition] Muller Automata
>A [DMA](Muller%20Automata.md) is a tuple:
>$$\mathcal{A}=(Q,A,\delta,q_0,\mathcal{F})$$
>- $Q$ the set of states
>- $A$ the alphabet
>- $\delta$ (determinisitic) transition functions
>- $q_0$ initial state
>- $\mathcal{F}$
>$Q,A$ and $q_0$ are defined as for the [DBA](Buechi%20automata.md)
>$\mathcal{F}$ is a subset of the powerset of $Q$
>i.e. $\mathcal{F}\subseteq 2^Q$ i.e. a set of subsets of $Q$
>
>The computation $\sigma$ of $\mathcal{A}$ on an $\omega\text{-word}$ $\alpha$ is successfull if and only if ($\iff$) $IN(\sigma)$ belongs to $\mathcal{F}$ i.e. $IN(\sigma)\in \mathcal{F}$.
>
>$\mathcal{A}$ accepts $\alpha$  if the computation $\sigma$ of $\mathcal{A}$ on $\alpha$ is successful.
>The language $L(\mathcal{A})$ is the set of all and only those $\omega\text{-words } \alpha$ accepted by $\mathcal{A}$. 

Example automat:

![](Muller%20Automata_image_1.png)