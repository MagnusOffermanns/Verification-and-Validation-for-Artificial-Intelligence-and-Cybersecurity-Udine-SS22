Notes about special cases of the $Until$ modality $U$:
- ==Special case 1== strong Until: $(p)U^{\exists}(q)$
	Means that that there must at some point in the future $q$ must go True. If not the result is $False$
- ==Special case 2==: non-strict Until: $(p)U_{\ge}(q)$
	Means that $q$ can also come true at time $t$. That means that $q$ and $p$ can be true at time $t$ then after this the values of $p$ and $q$ do not have an influene on the result of $U_{\ge}$. Summarized in natural language: Now is part of the future.

The $U$ we are using is the combination of both i.e. $U^{\exists}_{\ge}$.

>[!Note] The Until is the basic operator
>Later on we will find out that we can define the next operator $X$ using the Until operator $U$

### 0.1.1 Some more derived modalities
Lets define some more derived modalities:
#### 0.1.1.1 Infinitely many times
We want that $p$ is true infinitely many times: We denote the operator as $F^{\infty}(p)$:
A visual representation:
![](Verification%2030_image_1.png)

The solution is:
$F^{\infty}=G(F(p))$

To fullfill $G(F(p))$ we have to consider these steps:
1. To set $F(p)$ to True we need a occurence of $p=true$ some point in the future.
2. To fullfill $G$ the internal expression needs to be always true at some point. That means, so that $F$ is always true at a certain point there needs to be always a $p=true$ in the future, which means infinitely many times

A visualization fo this statement is the image below:
![](Verification%2030_image_2.png)

>[!Exercise] Expressing [Compassion](Compassion.md) in [PLTL](temporal%20logic.md).
>$p$: the state is enabled
>$q$: the state is taken
>$G(F(p)) \land F(q)$
>- $G(F(p))$ is only true if $p$ is infinitely many times in the future
>- $F(q)$ is only true if $q$ is true at some point in the future


#### 0.1.1.2 P before Q

$(p)B(q)$ $p$ gets positive at some point before $q$

We need to see a $p$ before the q becoming true.

![](Verification%2030_image_3.png)

No occurence of p is also forbidden

![](Verification%2030_image_4.png)

Solution:

$$\neg(\neg p)U(q)$$
1. What do we not want: We do not want what was illustrated in the image above. No $p$ before $q$. i.e. $(\neg p)U(q)$
2. Then we negate this as we want to prevent this from happening.

#### 0.1.1.3 Lets Simplyfy $F(F(p))$

Using the **strong** and **non-strict** definition of $U$.

Solution: $F(F(P))\equiv F(p)$

==Attention== This becomes different if we use a **strict** definition  of $U$.

If we assume strict $U$ the first occurence moves you at least 1 timestep into the future, the second $F$ moves you another timesteps in the future. I.e. the ranges where $p$ should become positive are of by one timestep. This is illustrated in the image below.

![](Verification%2030_image_5.png)

#### 0.1.1.4 What does $F(p \land Xq)$ mean?

It means that at some point in the future you find a place where $p[t]$ is true and $q[t+1]$ is true.

This can be seen in the image below:

![](Verification%2030_image_6.png)

#### 0.1.1.5 Are the two following formulas equivalent?
1. $F(p \land F(q))$ 
		First $p$ must become true than $q$
2. $F(p) \land F(q)$
		No ordering either $p$ or $q$ can go true first
3. $F(p \land q)$ 
	Both $p$ and $q$ need to go true at the same time

![](Verification%2030_image_7.png)

![](Verification%2030_image_8.png)

==Also:==
Using the simplifiaction of the non-strict definition of $F$ they are equivalent as:
$$F(p \land F(q)) \equiv F(p) \land F(F(q))) \equiv  F(p) \land F(q)$$

With a strict definition the two formulas are not equivalent.

#### 0.1.1.6 Are the two following formulas equivalent?

1. $G(p \implies F(Q))$
	Das bedeutet, jedes mal wenn ich ein $p$ finde muss ich ein $q$ in der Zukunft finden.
![](Verification%2030_image_9.png)
1. $G(G(p) \implies F(q)))$
	Ab einem gewissen Zeitpunkt muss $p$ immer true sein. des weiteren muss immer ein q in der zukunft sein i.e. infinitely many $q's$ after $p$ turned true.


That means that they are ==not equivalent==

---
30 b

---

# 1 [PLTL](temporal%20logic.md) Structures
$M:(S,x,L)$: discrete time/ there is an initial instant/ its infinite in the future
- $S$ set of States
	==finite==
- $x$: $\mathbb{N} \rightarrow S$ sequence of states
	Sometimes also called calculations
- $L:S \rightarrow POW(AP)$ labeling function
	Maps the Sets to a [Power set](Power%20set.md) of Propositional letters. For each state, it contains the propositional letters who are true in that state.

Notation:
If we want to denote all states from a certain timepoint we can denote it like this:

for all $i=0,1,2,3$ let $x^i=(s_i,s_{i+1},s_{i+2},...)$
$x^i$ contains all timepoints $\le i$. 

That means that $x^0$ are all states from the initial timepoint i.e. $x$.


## 1.1 Semantics

$M:(S,x,L)$ linear times structure

Definition of truth:
$$M,x \models p$$
- small letter (e.g. $p$): generic formula 
- capital letter (e.g. Q): Propositional letter

Examples:

- $M,x^i \models P \iff P \in L(s_i)$
	$P$ is true with respect to $M$ and $x^i$ if $P$ belongs to the labeling of the initial state of $s_i$. Why do we need to check if $P$ is in $L(s_i)$? $L(s_i)$ contains all Propositional letters that are true at instance $s_i$
- $M,x^i \models p \land q \iff P \in M,x^i \models p \text{ and } M,x^i \models q$
	 Standard definition
- $M,x^i \models \neg p \iff M,x^i \not \models P$
	also standard
- $M,x^i \models p U q \iff \exists j \ge i(x^j \models q \land \forall i \le k < j(x^k \models p))$
- $M,x^i \models X p \iff M,x^{i+1} \models P$

==REMARKS==
1. The semantics of the modal operators is a [First order formula](FO%20-%20First%20order%20logic.md) in a language whose individual variables range over states (see the semantics of $U$ or $X$).
2. We use strong and non-strict until. (see definition in [Verification 29](Verification%2029.md) or [Verification 30](Verification%2030.md)).
 3. If we define until as strict and strong we can define $X$ by using $U$ in the following way
	 $$(false)U^{\exists}_{\ge}(q)$$

>[!Theorem] [[Theorem 23]]
>The Monadic First-order theory of discrete linear order with first element (some soft of  discrete [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)) is equivalent to [PLTL](temporal%20logic.md)


#### 1.1.1.1 What about the past
We can redefine the modalities

- $X^-$ next in the negative direction. There is a problem if you are in the initial state, there is no past.
- $pU^-q$ A until a bit different direction (also refered to as $S$ as in Since) since q went positive p occured at least once 
- $F^-(p)$ p goes negative at some time in the past
- $G^-(q)$ at some point in the past q is always negative 

>[!Note]
>If we add the past [PLTL](temporal%20logic.md) does not get more [expressive](expressiveness.md), but we gain [Succinctness](Succinctness.md) we can write it with much less characters.

# 2 A [Tableaux](Tableaux.md) based decision procedure for [LTL](temporal%20logic.md)

## 2.1 Overview
- [[Point based temporal logics]]
- A [Tableaux](Tableaux.md) based decision procedure for LTL

## 2.2 [Point based temporal logics](Point%20based%20temporal%20logics.md)
### 2.2.1 Introduction
Explicit vs implicit methods for modal and temporal logics

>[!Note] Implicit methods
>In implicit methods the ==accessibility relation is built-in== into the structure of the [Tableaux](Tableaux.md).
>
>This is the case with [Tableaux](Tableaux.md) methods for linear and branching time temporal logics

>[!Note] Explicit methods
>Keep trak of the accessibility relatino by means of some sort o external device.
>
>This is the case with [Tableaux](Tableaux.md) methods for interval temporal logics where structured labels are associated with nodes to constrain the corresponding formula, or set of formulae, to hold only at the domain elements identified by the label. 

>[!Note] Declarative Methods
>Declarative Methods first generate all possible sets of subformulae of a given formula and then they eliminate some (possibly all) of them
>
>Declarative methods are generally easier to understand

Problem: Declarative methods create a lot of trash formulae

>[!Note] Incremental methods
>Generate only 'meaningful' sets of subformulae
>
>Incremental methods are more efficient

>[!Attention]
>Incremental methods are as powerfull as declarative methods

==We will use Implicit & Declarative methods==


 


