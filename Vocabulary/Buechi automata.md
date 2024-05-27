---
aliases: Buechi-automaton, Deterministic Buechi Automata, Deterministic Buechi Automata, DBA, NBA
---

# 1 [[Non deterministic]] [[Buechi automata]]
> [!note] definition
> A [[omega language|w-language]] $L \subseteq A^w$ is [[w-regular]] if it is a accepted by a [[Buechi automata]], that is there exists a [[Buechi automata]] $\mathcal{A}$ so that $L(A)=A$.


# 2 Deterministic [[Buechi automata]]

A [DBA](Buechi%20automata.md) is a Tuple: 
$$\mathcal{A}=\{Q,A,\delta,q_0,F\}$$
where $Q,A,q_0$ and $F$ are defined as for a [NBA](Buechi%20automata.md)
and:
$$ \delta: Q \times A \rightarrow Q$$

>[!note]
>$\Delta$ -> is a relation
>$\delta$ -> is a function

The computation $\sigma$ of $\mathcal{A}$ on an input $\omega-\text{word}$ $\alpha$ is successful if $IN(\sigma) \cap F = \emptyset$ . Which is similar to other infinite state machines, one state, which is in the set of Final states $F$ needs to be entered infinitely many times. Acceptance and Language defined by $\mathcal{A}$ are defined as for [NBA](Buechi%20automata.md).

==Reminder:$IN(x)$ is the set of states encountered  $IN\text{finitely}$ many times==

The main difference is that there are not many computations but only one computation.