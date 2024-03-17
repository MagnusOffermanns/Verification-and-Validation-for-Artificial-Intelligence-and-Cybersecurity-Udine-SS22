---
aliases: Closure under projection
---

>[!note] [[Lemma 14]] 
>An $\omega \text{-language } L \subseteq A^\omega$ is recognized by a [DMA](Muller%20Automata.md) if and only if ($\iff$) $L$ is a boolean combination (on $A^{\omega}$) of Languages of the form $\overrightarrow{w}$ where $w$ is a regular language.

Reasoning:  
If $w$ is a regular language the vectorial closure is recognized by a [DBA](Buechi%20automata.md). If it is recognized by a [DBA](Buechi%20automata.md) we know that it is also recognized by a [DMA](Muller%20Automata.md). And the [Theorem 18](Theorem%2018.md) says that [DMA](Muller%20Automata.md) is closed under boolean operations. As [the closedness property](Closed%20Formulas.md) describes if one has multiple languages are accepted by a [DMA](Muller%20Automata.md) also the boolean combination of them is accepted.