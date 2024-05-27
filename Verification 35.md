# 1 [[Branching time temporal logic]] alias [Computational Tree Logic](Branching%20time%20temporal%20logic.md)

Is simmilar to [LTL](temporal%20logic.md) but one state may have many successors. Time is still discrete.

Instead of only looking at one computation, we can look at all possible computations of a system.

## 1.1 Structure
What are the componenets of [CTL](Branching%20time%20temporal%20logic.md)

- $M:(S,R,L)$ Branching time structure
	- $S$ set of states
	- $R \subseteq S \times S$ binary relation of states
	- $L: S \rightarrow Pow(AP)$ labeling function

As $R$ is very general, the Branching time structure $M$ becomes a graph instead of a tree.

## 1.2 Language of [CTL](Branching%20time%20temporal%20logic.md)

$X$ and $U$ can be seen as quantifiers over states in a computation 

We add two components, which are quantifiers over computations:
- $A:$ For all futures
- $E:$ There exists a future

Summarizing we have:
- $X,U,F,G,\dots$ : states quantifiers
- $A,E:$ path quantifiers

[CTL](Branching%20time%20temporal%20logic.md) forces (Syntactically) two path quantifiers to be interleaved with one state quantifier.
This is a problem to its expressiveness, we will see some example later on.

>[!Note] 
>One can put state quantifiers right after each other e.g. $F(G(p))$. This does not hold for path quantifiers it does not make sense to put two of them right behind each other i.e. $AEF(G(x=3))$ is not a good sytax.

>[!Note] CTL\*
>Is simmilar to [CTL](Branching%20time%20temporal%20logic.md) but more expressive and unifies [CTL](Branching%20time%20temporal%20logic.md) and [LTL](temporal%20logic.md) but this will be a small topic of this class. It does not have the syntactical backdraw of having to have two statequantifiers between path quantifiers. For instance:
>$AX((p)U(q)\dots$ is valid in CTL\* but not valid in [CTL](Branching%20time%20temporal%20logic.md). 
>The formula in CTL would need an additional path quantifier i.e.
>$AX((p)U(q)E\dots$


## 1.3 Syntax of [CTL](Branching%20time%20temporal%20logic.md)
- $(s_1)$ $P \in AP$: All propositional letters are state formulae
- $(s_2)$ $p,q$ state formulae $\implies p \land q \neg p$ state formulae 
	if you have the state formula, and you [Conjunct](Conjunction.md), or negate them ($\neg$) it is still a state formula
- $(s_3)$ if $p$ is a [path formula](path%20formula.md) and $A$ or $E$ is applied it becomes a [state formula](state%20formula.md).
- $(s_4)$ if $p,q$ is a state formula if $X,F$ or $U$ are applied it becomes a path formula
	Why is this the case, because the formula is then not only active on the current state, but has an influence on future states

In [CTL*](Branching%20time%20temporal%20logic.md) the first three restrictions ($s_1$ till $s_3$)are the same as in normal [CTL](Branching%20time%20temporal%20logic.md). The last three differ

- $(s_1)$ $P \in AP$: All propositional letters are state formulae
- $(s_2)$ $p,q$ state formulae $\implies p \land q \neg p$ state formulae 
	if you have the state formula, and you [Conjunct](Conjunction.md), or negate them ($\neg$) it is still a state formula
- $(s_3)$ if $p$ is a path formula and $A$ or $E$ is applied it becomes a state formula.
- $(p_1)$ If we have a state formula $\varphi$ we can also consider it as a path formula.
- $(p_2)$ If we have a path formula $p,q$ if we use the [Conjunction](Conjunction.md) ($\land$) or negation ($\neg$) i.e. ($p\land q$ or $\neg p$)it stays a path formula.
- $(p_3)$ Given a path formulas one can still obtain other path formulas by applying $U$ or $X$ i.e. ($p,q$ path formula $\implies$ $X(p),(p)U(q)$ path formula)

>[!Note]
>In [CTL](Branching%20time%20temporal%20logic.md) the rule $s_4$ forces us to alternate between $A,E$ and $X,U$. In [CTL*](Branching%20time%20temporal%20logic.md) rule $p_3$ enables us to nest state quantifiers

## 1.4 Semantics of [CTL](temporal%20logic.md)
There are two forms of semantics one for [state formulas](state%20formula.md) and one for [path formula](path%20formula.md)s.

1. $M,s_0 \models p$ for $p$ state formula
2. $M,x \models p$ for $p$ path formula

### 1.4.1 [state formula](state%20formula.md) semantics
 $M,s_0 \models P \iff_{def} P \in L(s_0)$
 
 $M,s_0 \models p \land q \iff_{def}\quad M,s_0 \models p \text{ and } M,s_0 \models q$
 
 $M,s_0 \models \neg p \iff_{def} \quad M,s_0 \not \models p$
 
$M,s_0 \models E(p) \iff_{def} \quad \exists x = (s_0,\dots)(M,x \models p)$
	What does this mean? It means that there must exists a path with the initial state beeing $s_0$ so that $M,x$ model $p$

$M,s_0 \models A(p) \iff_{def} \quad \forall x = (s_0,\dots)(M,x \models p)$
 What does this mean? It means that in all states starting from $s_0$ $M,x$ must model $p$

### 1.4.2 [path formula](path%20formula.md) semantics

$M,x \models p \iff_{def} x=(s_0,\dots) \text{, and }p\text{ is a state formula and } M,s_0 \models p$
$M,x \models p \land q \iff_{def}\quad M,x \models p \text{ and } M,x \models q$
 
 $M,x \models \neg p \iff_{def} \quad M,x \not \models p$
 
$M,x \models (p)U(q) \iff_{def} \quad \exists i(M,x(i) \models q \land \forall (j<i)(M,x(j)\models p))$
 
$M,x \models X(p) \iff_{def} \quad M,x(1)\models p$

## 1.5 Examples:

<mark style="background: #FFB86CA6;">Example 1</mark>:
$$A(G(p \implies AF(q))))$$
Is a [[state formula]] because the first modality is an $A$ (see $s_3$)

What does the formula mean?
1. $AG$ for all future time strands the following holds
2. $AG(p \implies ...)$ When p is true at some point (the green dot in the image) from then on the rest of the formula must hold true
3. $$A(G(p \implies AF(q))))$$ Once $p$ is true on all time strands in the future $F(q)$ holds. That means that on all time strands $q$  has to be true at some point. This time point is painted in blue in the image below.

If $p$ turns true again after we saw the $q$ turn true, $q$ will have to be true at some point after the $n^{th}$ occurence of $p$


![](Verification%2035_image_1.png)


>[!Note] 
>Later on we will find out that the set of all [CTL](Branching%20time%20temporal%20logic.md) formulas only contain [state formulas](state%20formula.md) i.e. one needs to start either with an $A$ or $E$

One takeaway:
$A$ -> all future paths
$G$ -> all future states
$AG \equiv \text{ everywhere}$ 

A lot of formulas start like this. Because we want to apply a condition everywhere.

Example 2:
$$A(G(p \implies EF(q))))$$

The difference to the example above is that $q$ does not have to appear after the $p$ in all time-strands but only in one.

Also in the image below I wanted to point out that whenever there is a $p$  a $q$ has to follow meaning that they always have to appear in pairs. Therefore a second $p$ and $q$ pair is painted in the figure.

![](Verification%2035_image_2.png)

What is the [LTL](temporal%20logic.md) counterpart  of the formula:
$$A(G(p \implies AF(q))))$$
The corresponding [LTL](temporal%20logic.md) formula is:
$$G(p \implies F(q))$$

==Example 3:==
$$E(F(q)) \implies E(F(E(G(q)))) $$

![](Verification%2035_image_3.png)

One decisive difference is as $E(F(E(G(q))))$ is not in the bracket of the first $E(F(\dots$ it can be in another branch, and must not be in the same branch as in Example 1 and 2.

One takeaway:
$F$ -> one of the future paths
$G$ -> all future states
$FG \equiv \text{ somewhere}$

==Exercise 4:==
$$A(G(p \implies E(X(p)))) \implies A(G(p \implies E(G(p))))$$

1. $A(G(p \implies E(X(p))))$
	Everywhere where we find $p$ to be true, in all branches that follow in the next timestep there must be a branch where  $p$ must be true. This recursively defines that we find a $p$ after each $p$ in one of the branches.
	![](Verification%2035_image_4.png)
2. $A(G(p \implies E(G(p))))$
	This means that therealways needs to be a path where $p$ is true. 
	![](Verification%2035_image_5.png)

As we have already defined in the first formula that we have an infinite amount of $p$ also the second part of the formula is always true. That means that this formula is always true i.e. [Valid](Validity.md).

==Exercise 5: Important example==:
$$A(G(p \implies E(F(q))))$$

![](Verification%2035_image_6.png)

When we find a $p$ we need to find a $q$. When we find another $p$, we  need to find a $q$ but this one could be on another path.

There is a way of satisfying this formula without having a infinite path with infinite occurences of $p$ and respectively $q$. But by having an infinite many paths each with a finite number of occurences of $q$ the limit of $p/q$ occurences  is infinite.

Summarizing: We have infinitely many timestrands with a finite number of $p/q$ occurences. But as we have an infinite number of timestrands we still have an infinite amount of $p/q$ on all of the timestrands.

This is one of the differences of [LTL](temporal%20logic.md) and [CTL](temporal%20logic.md).
- In [LTL](temporal%20logic.md) we need an infinite amount of $q$s to satisfy infinite occurences of $p$.
- In [CTL](temporal%20logic.md) we are able to satisfy such a formula even if we do not have an infinite number of occurences of $p/q$.

>[!Note]
>A [LTL](temporal%20logic.md) formula that states the same condition as the [CTL](temporal%20logic.md) formula from above, does not exist.


Now the question is: Is [CTL](temporal%20logic.md) clearly more expressive as [LTL](temporal%20logic.md)?

Yes there is stuff we can do only in [LTL](temporal%20logic.md).
In [CTL](temporal%20logic.md) we need to alternate between State and path quantifiers. i.e. $AGAFEG(p)$. In [LTL](temporal%20logic.md) we can put two state quantifiers right behind each other for instance the very important:
- $G(F($ 
	Infinitely many times
- $F(G($
	Sometimes in the future the statement  is always true

We need these two statements to define [Justice](Justice.md) and [Compassion](Compassion.md). For the solution of this problems see [Verification 30](Verification%2030.md) and [Exercises session 30](Exercises%20session%2030.md).

>[!Note]
>In terms of [expressiveness](expressiveness.md) [CTL](temporal%20logic.md) and [LTL](temporal%20logic.md) are incomparable. There are things that the one can do and the other one not, an vice versa.

==Exercise 6==
An example of a [CTL*](temporal%20logic.md) formula
$$A(G(p\implies E(X(F(p)))))\implies(p \implies E(G(F(p))))$$

We see that $X(F(...$  and $G(F(...$ are directly behind each other this is ==Not possible in [CTL](temporal%20logic.md).==

![](Verification%2035_image_7.png)

We can assume that if the formula is true, if we find a $p$ we find infinite $p$s.

==Why do we need the $X$?== Why do we not just write $A(G(p\implies E(F(p))))$?

This is due to the definition of the $Until$ i.e. the operator $(q)U(p)$. We are using the non-strict definition. That means that the Until can refer to the the occurence of $p$ at time $t=0$ in the same moment. By using the $X$ we force the formula to look for a $p$ in the future. 


## 1.6 Variants of [CTL](temporal%20logic.md) and [CTL*](temporal%20logic.md)

### 1.6.1 PCTL*
Extension of [CTL*](temporal%20logic.md) with past operators (over paths).

One can for instance say that certain things for th past must be true.

### 1.6.2 DCTL*
Extension of [CTL*](temporal%20logic.md) with (explicit) successors.

It is possible to translate every tree into a binary tree i.e. a tree with two successors. 
After translating the tree into a binary tree one can refer to specific children of a node for instance "left successor" or "right successor". 

### 1.6.3 PDCTL*
Extension of [CTL*](temporal%20logic.md) with both past operators and (explicit) successors


>[!Note] [CTL](temporal%20logic.md) and [CTL*](temporal%20logic.md)formulas
>The set of state formulas is equivalent to the set of [CTL](temporal%20logic.md)/[[CTL*]] formulas.
>This has the effect that the outer most modifier needs to be a path quantifier i.e. $A\dots$ or $E\dots$

