# 1 Outline


**What is the goal of this lesson:**
We want to find a mechanism with which we can decide [Satisfiability](Satisfiability.md) for a [LTL](temporal%20logic.md).

In this field we call this ==completeness==.

Also we want to show [Validity](Validity.md).

## 1.1 [Point based temporal logics](Point%20based%20temporal%20logics.md)

Gave an overview over current research.

The [Satisfiability](Satisfiability.md) problem for [PLTL](temporal%20logic.md)/[LTL](temporal%20logic.md) is [PSPACE](PSPACE) complete.

Over bounded models of polynomial length [Satisfiability](Satisfiability.md) is [NP-complete](NP%20problems.md).

## 1.2 A [Tableaux](Tableaux.md) based decision procedure for [LTL](temporal%20logic.md)

The decision procedure for [LTL](temporal%20logic.md) we present here is covered in :

![](Verification%2031_image_1.png)

## 1.3 Expansion rules and closure

### 1.3.1 Expansion

We have already encountered the following modalities:
- $G(p) \approx p \land X(G(p))$
	A operator that is true if a variable $p$ is always true in the future the shortform for this is $G(P)$
- $F(p) \approx p \lor X(F(p)$
	A operator that is only true if $p$ gets true sometimes in the future we denote this as $F(p)$.
- $(p)U(q) \approx q \lor (p \land X((p)U(q)))$
	$(p)U(q)$ is only true if $p$ is true until $q$ is true. If $p$ ever goes False before $q$ becomes true, the statement is false. The statement is also only true if $q$ ever becomes true in the future. If $q$ stays $False$ until infinity $(p)U(q)[t]$ also stays False.

In this round we will expand them:

1. $G(p) \approx p \land X(G(p))$
	The state does not only have to be always true in the future $[t+1]$, but also not i.e. at timepoint $[t]$
2.  $F(p) \approx p \lor X(F(p)$
	To fullfill $F(P)$, $p$ does not need to be true at a future time, but can also be true at timepoint $[t]$.
3. $(p)U(q) \approx q \lor (p \land X((p)U(q)))$
	Either $q$ is true now (i.e. $[t]$) or until is shifted by one time from $[t]$ to $[t+1]$. To still force $p$ to be true at time $[t]$ we logically and it with the $U$ operator.

### 1.3.2 [Closure Property](Theorem%205.md) of a formula
Closure $\phi_\varphi$ of a formula $\varphi$ 

We look for the smallest set of formulas that fullfill the following requirements:
1. $\varphi \in \phi_\varphi$
	My formula is part of the closure
2. for every $p \in \phi_\varphi$ and subformula $q$ of $p$ it holds that $q \in \phi_\varphi$
	Every subformula of our formula is part of the closure
3. for every $p$ \in $\phi_\varphi$ it holds that $\neg p \in \phi_\varphi$ and that $\neg\neg p \equiv p$
	Not only our formula but also its negation is in the closure
4. for every $\psi \in \{G(p),F(p),(p)U(q)\}$ if $\psi \in \phi_\varphi$ then $X(\psi) \in \phi_\varphi$
	==Attention specific for [temporal logic](temporal%20logic.md)== 
	For every formula of the form $\{G(p),F(p),(p)U(q)\}$ part of our set $\phi_\varphi$, we need to add the respective next operator. That means: for $G(P)$ we need to add $X(G(p)$, for $F(P)$ we need to add $X(F(P))$ and so on.


Lets define an example:

$\varphi:$  $G(x) \land F(\neg p)$

>[!Note] [Satisfiability](Satisfiability.md)
>$\varphi$ is not [Satisfiable](Satisfiability.md)

The closure is $\phi_\varphi = \phi_{\varphi}^{+} \cup \phi_{\varphi}^{-}$ 

Therefore we follow the above steps:

1. The formula itself is part of the closure
	$\phi_{\varphi}^{+}=\{\varphi\dots\}$
2. Every subformula is part of the closure
$\phi_{\varphi}^{+}=\{\varphi,G(p),F(\neg p) ,p,\dots\}$
4. We add the formulas specific for the [temporal logic](temporal%20logic.md)
	$\phi_{\varphi}^{+}=\{\varphi,G(p),F(\neg p) ,p,X(G(p)),X(F(\neg p))\}$
	
1. Adding the negation as well as checking that and$\neg\neg p \equiv p$
	$\phi_{\varphi}=\phi_{\varphi}^{+} \cup \phi_{\varphi}^{-}$
	while $\phi_{\varphi}^{+}$ is:
	$\phi_{\varphi}^{-}=\{\neg \varphi,\neg G(p),\neg  F(\neg p),\neg  X(G(p)),\neg  X(F(\neg p),\neg p)\}$

>[!Note] Remark on the size of the closure 
>Max size: $|\phi_\psi| \le 4 \cdot |\psi|$
>The element that adds the most elements are:
>$G,F$ and $U$ we need to add for instance for $G$
>$$G -> \{G(p),\neg G(p),X(G(p)),\neg X(G(p))\}$$

### 1.3.3 alpha tables and beta tables
$\alpha$-tables -> universal rules
$\beta$-tables -> existential rules

Lets first look at the $\alpha$-table:

![](Verification%2031_image_2.png)

We have that an $\alpha$-formula holds at position $j$ if and only if ==all of== $k(\alpha)$ formulae hold at $j$. Where $j$ is the row of the table.

![](Verification%2031_image_3.png)

We have that a $\beta$-formula holds at position $j$ if and only if either the $k_1(\beta)$ or $k_2(\beta)$ or both hold at row $j$.

### 1.3.4 Atoms
We define atoms always over a formula. We write it as a $\varphi$-atom is a atom over $\varphi$. 

What is a atom?

A $\varphi$-atom is a <mark style="background: #014E11F2;">subset</mark> of the [Closure](Closure.md) i.e. $A \in \phi_\varphi$ satisfying:
1. $R_{sat}:$ the conjunction of all [local formulae](local%20formula.md) in $A$ is [Satisfiable](Satisfiability.md).
	By only looking at [local formulae](local%20formula.md) one eliminates contradiction that can occur through temporal operators (e.g. next, until etc.)
2.  $R_{\neg}:$ for every $p$ in the closure (i.e. $p\in \phi_\varphi$), $p$ is only part of $A$ (i.e. $p \in A$) if and only if ($\iff$) the negation of the formula is not in the Atom (i.e. $\neg p \not \in A$)
	This means that for every $p \in \phi_\varphi$ a $\varphi$-atom must contain either $p$ or $\neg p$.
3. $R_{\alpha}:$ for every $\alpha$ formula $\alpha \in \phi_\varphi$, $\alpha$ is only in the Atom (i.e. $\alpha \in A$ if and only if ($\iff$)$k(\alpha) \subseteq A$ (e.g. $G(p) \in A$ if and only if both $p \in A$ and $X(G(p)) \in A$)
4. $R_{\beta}:$ for every $\beta$-formula $\beta \in \phi_\varphi$, $\beta$ is only in the Atom $A$ if and only if ($\iff$) either $k_1(\beta) \in A$ or $k_2(\beta) \in A$ or both.


==Example 1:==
$A_1=\phi_{\varphi}^{+}=\{\varphi,G(p),F(\neg p) ,p,X(G(p)),X(F(\neg p))\}$
1. $R_{sat}$ -> satisfiable only $p$ is a [local formula](local%20formula.md)
2. $R_{\neg}$ -> only contains $p$
3. $R_{\alpha}$ -> satisfiable
4. $R_\beta$ -> satisfiable
 
$A_2=\phi_{\varphi}^{+}=\{\varphi,G(p),F(\neg p) ,p,X(G(p)),\neg X(F(\neg p))\}$ 
1. $R_{sat}$ -> satisfiable only $p$ is a [local formula](local%20formula.md)
2. $R_{\neg}$ -> only contains $p$
3. $R_{\alpha}$ -> not satisfiable
	Both subformulae  of a $\alpha$-formula ($k_\alpha$) must be part of the Atom. The counterexample is $G(p)$ the two subformulae are: $X(G(p))$ and $p$. $X(G(p))$ is part of $A$ (i.e. $K_{\alpha 1} \in A = X(G(p)) \in A_2$ but $p$ the second $K_{\alpha2} \not \in A = p \not \in A_2$. As $\neg p$ is in $A_2$ after $R_\neg$ we can not add $p$
4. $R_\beta$ -> satisfiable

The intended meaning of atoms

Atoms are used to represent maximal [[mutually satisfiable]] sets of fomulae. 

>[!Definition]
>A set of formulae $S \subseteq \phi_\varphi$ is [mutually satisfiable](mutually%20satisfiable.md) if there exists a model $\sigma$ and a timepoint $t \ge 0$ such that every formula $p \in S$ holds at position $t$

>[!Note] Proposition
>For any set of [mutually satisfiable](mutually%20satisfiable.md) formula subset of a [Closure](Closure.md) (i.e. $S \subseteq \varphi$ ) there exists a $\varphi$-atom $A$ such that $S \subseteq A$

==Problem:== <mark style="background: #FF5582A6;">The opposite does not hold!</mark>
It may happen that $S \subseteq \phi_\varphi$ and there exists a $\varphi$-atom $A$ such that $S \subseteq A$, but $S$ is not mutually satisfiable (an example would be $X(p) \land X(\neg p$).


i.e. We have a [mutually satisfiable](mutually%20satisfiable.md) set -> there exists a $\varphi$-atom where the mutually satisfiable set is part of the atom.

But not all Atoms are [mutually satisfiable](mutually%20satisfiable.md).

---
V&V 31 b Anfang

---

### 1.3.5 [[elementary formula]]s
>[!Definition] [elementary formulae](elementary%20formula.md)
>[Basic formulae](elementary%20formula.md) are propositions or formulae of the Form $X(p)$

>[!Note] Property of basic Formulae
>The presence or absence of basic formulae in a n Atom $A$ determine the presence or absence of all other closure formuale in $A$

Example:
$$\varphi: G(p) \land F(\neg p)$$

The closure contains 3 basic formulae:
1. $X(G(p))$
2. $X(F(\neg p))$
3. $p$

Lets suppose that $X(G(p) \in A$ ,$X(G(\neg p)) \in A$ while $p \not \in A$

Hereby we can do some deductions:
- From $p \not \in A$ $\Rightarrow$ $\neg p \in A$
- From $p \not \in A$ and $X(G(p)) \in A$ $\Rightarrow$ $\neg G(p) \in A$
	Here we use the $R_\alpha$ rule to determine the statement. We apply $k_\alpha(X(G(p))$ and get the following two formulas, which both need to be in the atom, $k_{\alpha,1}=p$ as we know from the point above that $p$ is not in the Atom it does not matter whether $k_{\alpha,2}=G(p)$ is part of the atom because as of $R_\alpha$ both formulae need to be part of the atom. But now we apply $R_\neg$ we know that the negation needs to be in the atom i.e. $\neg G(p)$
- From $\neg p \in A$ and $X(F(\neg p))  \in A \Rightarrow$  $F(\neg p) \in A$
	Using the $R_\beta$ rule we can conclude that $F(\neg p) \in A$
- From $G(p) \not \in A$ and $F(\neg p) \in A $, it follows that $\neg \varphi \in A$
	We use the $R_\alpha$ rule to conclude that $\varphi \not \in A$
	$$\varphi: G(p) \land F(\neg p)$$ i.e. $k_\alpha(G(p) \land F(\neg p))=G(p),F(\neg p)$ as $G(p) \not \in A$ and both Formulae need to be in the atom, we can state that $\varphi \not \in A$


### 1.3.6 Lets build the [Tableaux](Tableaux.md)

We build a [Tableaux](Tableaux.md) based on a formula $\phi$.

What are the nodes and edges of a [Tableaux](Tableaux.md):

The nodes of $T_\varphi$ are the atoms of $\varphi$.
There exists an edge between nodes, if the two respective atoms $A$ and $B$ if for every $X(p) \in \phi_\varphi$ i.e. [Basic formula](elementary%20formula.md) in the [Closure](Closure.md) if $X(p) \in A \iff p \in B$
If we have a negation i.e. $\neg X(p) \in A \iff \neg p \in B$

This is the [Tableaux](Tableaux.md):
![](Verification%2032_image_14.png)

Lets consider the edge of $A_2$. 
	As $X(F(\neg p))$ is in $A_2$ we need to look if $F(\neg p)$ is in $A_2$. Indeed it is! Therefore we have edge from $A_2$ to $A_2$.
	 Further we have $\neg X(G(p))$ here we need to make sure that $\neg G(p)$ is in the target node and indeed it is.

>[!Attention]
>One has an infinite number of infinite paths in the [Tableaux](Tableaux.md).

What can we see from the Atoms:
- There is never $p$ and $\neg p$ in one Atom
- Universal conditions are provided by $R_\alpha$ and the rules of the edges


>[!question]  how does the [Tableaux](Tableaux.md) look like for $\neg \varphi$?
>Because the [Closure](Closure.md) is equivalent for $\varphi$ and $\neg \varphi$  the [Tableaux](Tableaux.md) are also the same for $\varphi$ and $\neg \varphi$,

Question we will answer in the next classes. If the [Tableaux](Tableaux.md) are the same, how do differentiate between finding a model for $\varphi$ and finding a model for $\neg \varphi$.

### 1.3.7 Models and [Tableaux](Tableaux.md) paths

>[!Note] [[Induced Path]]
>Given a model $\sigma$ of $\varphi$ the infinite path $\pi_\sigma: A_0,A_1,...$ in $T_\varphi$ is induced by $\sigma$ if for every position $j \ge$  and every $p \in \phi_\varphi(\sigma,j) \models p \iff p \in A_j$ (in particular $\varphi \in A_0$)


That means that we have the following requirements for the [Induced Path](Induced%20Path.md).

The infinite path through the states $A_0,A_1\dots$ through in the [Tableaux](Tableaux.md) $T_\varphi$ is induced if at every timepoint after a timepoint $[j]$ greater 0 and every formula $p$ in the closure ($p \in \phi_\varphi$) is a model (i.e. true) and the formula $p$ is in $A_j$.

>[!Note] Proposition
>Given a formula $\varphi$ and a [Tableaux](Tableaux.md) $T_\varphi$ for it, for every model $\sigma: s_0,s_1, \dots$ of $\varphi$ there exists an infinite path $\pi_\sigma:A_0,A_1,\dots$ in $T_\varphi$ such that $\pi_\sigma$ is induced by $\sigma$


Sketch of the proof:
![](Verification%2031_image_5.png)

>[!Note] An immediate consequence
>Since $\sigma$ is a model of $\phi$ we have that $(\sigma,0) \models \phi$ and thus $\phi \in A_0$

We call this initial satisfiability

i.e. **The opposite does not hold:** not every infinite path in  $T_\varphi$ is induced by some model $\sigma$

Good but not the end of the story:
Now we know that if there is a model there is a path. ==We need to still reject bad paths to find the one that models the formula!==

A bad path that is not induce by a Formula:

When we remember the Tableux from before:

![](Verification%2033_image_1.png)

And lets consider the path $A_7^\omega$ (i.e. we stay in $A_7$ for ever). This is not a good path.

We already know that it dies because of the $\beta$ request.

We only need to check $A^\omega_7$ as it is the only state that has the original formula $\varphi$ in it.

![](Verification%2031_image_7.png)


>[!Definition] [[Promise]]
>A formula $\psi \in \phi_\varphi$ is said to [[Promise]] a formula $r \iff \psi$ has one of the following forms:
>1. $F(r)$
>2. $(p)U(r)$
>3. $\neg G \neg r$
>(1 and three are saying the same written differently)

>[!Note] Property 1
>if $(\sigma,j) \Vdash \psi$ then $(\sigma,k) \models r$, for some $k \ge j$

If $\sigma$ makes the formula $\psi$ at timepoint $j$ true, then at some point in the future named $k$ ($k \ge j$) it must be true again i.e. ($(\sigma,k) \vdash r$)

>[!Note] Property 2
>The model $\sigma$ containes infinitely many positions $j \ge 0$ such that:
>$$(\sigma,j) \Vdash \neg \psi \text{ or } (\sigma,j) \Vdash r$$

If a formula is a model ($\sigma$) it has to have either infinitely many positions $j \ge 0$ where the promising formula is false ($\neg \psi$) or the promising formula ([Promise](Promise.md)) is true ($(\sigma,j) \Vdash r$)









