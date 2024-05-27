---
aliases:
  - Quantified Boolean formulas
---


<mark style="background: #014E11F2;">Vocabulary:</mark> 
- Boolean variables $\sum = \{p,q,r...\}$
- Boolean connectives $\land,\lor,\neg,\iff,\implies$
- $\forall,\exists$ Quantifiers

<mark style="background: #014E11F2;">Syntax:</mark> 
$$\phi = p|q|...|\phi \land \phi|\phi \lor \phi|\neg\phi| \phi \iff \phi|\phi \implies \phi|\exists p \phi|\forall p \phi$$

<mark style="background: #014E11F2;">semantics</mark> :
describes when $S \models \phi$ for $S: \sum \implies \{\text{True,False}\}$

| $S \models p$                   | $\iff$ | $S(p)=True$                                                                        |
| ------------------------------- | ------ | ---------------------------------------------------------------------------------- |
| $S \models \phi_1 \land \phi_2$ | $\iff$ | $S \models \phi_1 \text{ or } S \models \phi_2$                                    |
| ...                             |        |                                                                                    |
| $S \models \exists p \phi$      | $\iff$ | $S'\models \phi \text{ for some } S' \in \{S[p:=\text{true}],S[p:=\text{false}]\}$ |
| $S \models \exists p \phi$      | $\iff$ |                     $S'\models \phi \text{ for every } S' \in \{S[p:=\text{true}],S[p:=\text{false}]\}$ |                                                               |


