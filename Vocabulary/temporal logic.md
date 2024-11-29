---
aliases:
  - linear time temporal logic
  - branching time temporal logic
  - PLTL
  - CTL
  - CTL*
  - Propositional Linear Temporal Logic
  - LTL
---
# 1 Propositional Linear Temporal Logic
## 1.1 Syntax
- $P,Q$ Propositional letters $AP$
- $\neg,\land$ Porpositional connectives
- $X$: Next, $U$: until temporal connective
	- $X$: what does the Next operator mean?
		 $X(p)[t]$ (i.e. $X(p)$ at time $t$)is true depending on the state of $p$ in the next time step : If $p[t+1]=False$ -> $X(p)[t]=False$. If  $p[t+1]=True$ -> $X(p)[t]=False$. $X(p)$ does only depend on the value of $p$ in the future state, it does not depend on the state of $p$ at timepoint $t$ i.e. $p[t]$.
	- $U$: what does the until operator mean?
		$U$ has two arguments we write it like this  $(p)U(q)$.
		$(p)U(q)$ is only true if $p$ is true until $q$ is true. If $p$ ever goes False before $q$ becomes true, the statement is false. The statement is also only true if $q$ ever becomes true in the future. If $q$ stays $False$ until infinity $(p)U(q)[t]$ also stays False.
- Formulae: $P,p\land q, \neg p, Xp,pUq$

Other important operators:
$F$: p will be true at some point in the future
$$F(p) \equiv (True)U(p)$$
$G$: p will be always true in the future
$$G(p) \equiv \neg F(\neg p)$$

>[!note] syntax in modal logic
>$X \equiv \bigcirc$
>$G \equiv \square$
>$F \equiv \diamondsuit$
>![](temporal%20logic_image_1.png)



## 1.2 Satisfiability
The [Satisfiability](Satisfiability.md) problem for [PLTL](temporal%20logic.md)/[LTL](temporal%20logic.md) is [PSPACE](PSPACE) complete.

Over bounded models of polynomial length [Satisfiability](Satisfiability.md) is [NP-complete](NP%20problems.md).


# 2 CTL & CTL*

$X$ and $U$ can be seen as quantifiers over states in a computation 

We add two components, which are quantifiers over computations:
- $A:$ For all futures
- $E:$ There exists a future

Summarizing we have:
- $X,U,F,G,\dots$ : states quantifiers
- $A,E:$ path quantifiers


<mark style="background: #FFB86CA6;">Example</mark>:
$$A(G(p \implies AF(q))))$$
Is a [[state formula]] because the first modality is an $A$ (see $s_3$)

What does the formula mean?
1. $AG$ for all future time strands the following holds
2. $AG(p \implies ...)$ When p is true at some point (the green dot in the image) from then on the rest of the formula must hold true
3. $$A(G(p \implies AF(q))))$$ Once $p$ is true on all time strands in the future $F(q)$ holds. That means that on all time strands $q$  has to be true at some point. This time point is painted in blue in the image below.

If $p$ turns true again after we saw the $q$ turn true, $q$ will have to be true at some point after the $n^{th}$ occurrence of $p$


![](temporal%20logic_image_2.png)

