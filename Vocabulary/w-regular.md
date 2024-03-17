---
aliases: w-regular-language, w-language,w-regular-expression
---

A [[omega language|w-language]] $L \subseteq A^w$ is [[w-regular]] if it is a accepted by a [[Buechi automata]], that is there exists a [[Buechi automata]] $\mathcal{A}$ so that $L(A)=A$. 


![[example buechi automaton.png]]

A Büchi automaton with two states,  $q_0$ and  $q_{1}$, the former of which is the start state and the latter of which is accepting. Its inputs are infinite words over the symbols $\{a,b\}$. As an example, it accepts the infinite word ${\displaystyle (ab)^{\omega }}$ , where  $x^{\omega }$ denotes the infinite repetition of a string. It rejects the infinite word ${\displaystyle aaab^{\omega }}$
