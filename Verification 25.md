
> [!note] [[Theorem 15]] a.k.a. [[Theorem 15|Buechis-theorem]]
> An [[w-regular|w-language]] $L \subseteq A^w$ is [[w-regular]] if and only if ($\iff$) it is definable in [S1S](Monadic%20second%20order%20of%20one%20sucessor.md). 

==Proof:==
1. ==Direction ($\implies$) ==
(If a  [[w-regular|w-language]] $L \subseteq A^w$ is [[w-regular]]  it is definable in  [[Monadic second order of one sucessor|S1S]].)

Let $\mathcal{A}=(Q,A,\Delta,q_0,F)$ be a [[Buechi automata|Buechi-automaton]] that recognizes a given [[w-regular|w-language]] $L \subseteq A^w$.

Let:
- $Q=\{0,1,2,...,n\}$
- $q_0=0$

We are going to write a [[Logical Sentence]] of the form (no [[free variables]]):
$$\exists Y_1\exists Y_2...\exists Y_m \varphi(Y_o,Y_1,...Y_M)$$
This $S1S_A$ formula such that for all [[omega-words|w-word]] $\alpha \in A^w$ is a model of such a formula $\iff$ it is accepted by $\mathcal{A}$.

The sets $Y_i$  represent the positions where the computation of $\mathcal{A}$ is at the state $i$. This means that for every position we have a state $i$ and a symbol $x$.

The formula $\varphi$ consists of three [[Conjunction]]s.

1. $\varphi_1=\{Y_0,Y_1....,Y_m\}= 0 \in Y_0 \land  \neg \exists y (y \in Y_i \land y \in Y_j)$
	The first formula that the computation starts in the initial state 0, the second formula means that the computation at every position can only be in one state (The sets $Y_0$ till $Y_m$ dont share any members i.e. they are [[Disjoint]]).
2. $\varphi_2=\{Y_0,Y_1....,Y_m\}=\forall x \bigvee\limits_{(i,a,j) \in \Delta} (x \in Y_i \land x \in Q_a \land x+1 \in Y_j)$ ([[Rule of Consequentiality]])
	$i,j$ are states, $a$ is an element of the alphabet $A$. It means that for all states $x$ there must be a transition and at the $x^{th}$  position we find a the relevant symbol ($a$) and the next state at which we arrive in (next state) must be in the next state $Y_j$. The big disjunction says that there must be at least one of those transitions.

![[Verification 25_image_1.jpeg|600]]
 
3. $\varphi_3=\{Y_0,Y_1....,Y_m\}=\bigvee \limits_{i \in F} \forall x \exists y(x<y \land y \in Y_i)$ ([[Acceptance condition]])
	This means that for every state $x$ we need a state  $y$ that lies ahead of $x$ (is a consecutive) that is part of the final state $F$. The distance between $x$ and $y$ might be 1 but could also be $n$ the important thing is that it lies in the future.

The sentence we are looking for are the three formulas above combined:
$$\exists Y_0 \exists Y_1....\exists Y_m \varphi_1=\{Y_0,Y_1....,Y_m\} \land \varphi_2=\{Y_0,Y_1....,Y_m\} \land $\varphi_3=\{Y_0,Y_1....,Y_m\}$$

Hereby we show that each [[w-regular]] [[w-regular|w-language]] can be expressed as a [[Monadic second order of one sucessor|S1S]] formula! Which concludes our prove of the first direction.

2. ==Direction ($\leftarrow$)== A [[Monadic second order of one sucessor|S1S]] formula can be expressed as a [[Buechi automata|Buechi-automaton]]

We are going to do some preliminary work to simplify the translation of formulas into automate. We replace [[Monadic second order of one sucessor|S1S]] formulas with $S1S_0$ formulas where $S1S_0$ formulas only admit second order variables and atomic formulas of the forms:
- $X \subseteq Y$
- $SUCC(X,Y)$ where $X=\{x\}$ and $Y=\{y\}$ and $y=x+1$

We prove that $S1S_0$ and [[Monadic second order of one sucessor|S1S]] are equivalent.
1. direction $S1S_0 \rightarrow S1S$ 
	$X \subseteq Y \equiv \forall x (x \in X \implies x \in Y)$
	$SUCC(X,Y) \equiv \exists x \exists y (x \in X \land \neg \exists x' (x' \in X \land x' \not = x)) \land (y \in Y \land \neg \exists y' (y' \in Y \land y' \not = y)) \land x+1=y$
2. direction $S1S \rightarrow S1S_0$
	Some useful short hands:
	- $X=Y \equiv X \subseteq Y \land Y \subseteq X$
	- $X \not = Y \equiv \neg (X=Y)$
	- $Sing(X) \equiv \exists Y (Y \subseteq X \land Y \not = X \neg \exists Z(Z \subseteq X \land Z \not = X \land Z \not = Y))$
		Explanation of the singleton: The [[Singleton]] (a set containing only one element has only two subsets, itself and the empty set ($\emptyset$)), the first part ($Y \subseteq X \land Y \not = X$) says that there must be a subset that is not the entire set,  referring to the  the empty set, the second part (the one with $Z$ defines that there should be no other subset apart from  $Y \equiv \emptyset$) and $X$ itself.)
	
---
==25b==

---
A couple of preliminary writings:
1. We force the $+1$ function to occur only in formulas of the form $x+1=y$
	Example: We rewrite the formula $x+1\in X$ as $\exists y ((x+1=y) \land (y \in X))$
	Example: $x+1+1 \in X$ becomes $\exists y \exists z (x+1=y \land y+1 =z \land z \in X)$
2. We eliminate $0$ and $<$
	$x<y$ becomes $\forall X (x+1 \in X \land \forall z (z \in X \implies z+1 \in X )) \implies y \in X$
	$x=0$ becomes : $\forall y (x<y \lor x=y)$

At the end of this rewriting formulas are of the following forms:
$x=y$, $x+1=y$, $x \in Y$ 

We need to be able to rewrite this $S1S$ formulas as [[Monadic second order of one sucessor#1 $S1S_0$|S1S_0]] formulas

$x=y \rightarrow X=Y \land Sing(X) \land Sing(Y)$
$x+1=y \rightarrow SUCC(X,Y)$  
$x \in Y \rightarrow X \subseteq Y \land Sing(X)$

To complete the translation we need to eliminate [[FO - First order logic|FO]] variables from quantifications.

We transform $\exists$ and $\forall$ of [[FO - First order logic|FO]] variables in existential or universal quantification of Second order ones restricted to [[Singleton]]s. Every existential quantifier becomes a second order quantifier with a check if it is [[Singleton]]. Every universal quantifier gets a singleton check and a implies to only be true if $X$ is a [[Singleton]].

Example:
$\exists x(...) \rightarrow \exists X(Sing(X) \land ....)$
$\forall x(...) \rightarrow \forall X(Sing(X) \implies .... )$

Another example:
	$$\forall x \exists y(x+1 =y \land y \in Z)$$
	Can be rewritten as:
	$$\forall X  (Sing(X) \implies \exists Y (Sing(Y) \land SUCC(X,Y) \land Y \subseteq Z))$$
Now we can restrict our attention to [[Monadic second order of one sucessor#2 $S1S_0$|S1S0]].

The proof is by induction on the structure of $S1S_0$ Formulas:

==First case:==
$X_1 \subseteq X_2$

How can we express it as an automaton? A automaton that finishes its computation positively if $X_1 \subseteq X_2$
==Example:==
![[Verification 25_image_2.jpeg|400]]

$X_1=\{1,2\}$
$X_2=\{1,2,3\}$

![[Verification 25_image_3.jpeg]]



==Second case==
$SUCC(X,Y)$

![[Verification 25_image_4.jpeg]]

Only one sequence that is allowed are Infinite zeros, then $X_1$ turns to one and then directly in the next step $X_1$ goes to 0 and $X_2$ goes to 1. Afterwards $0,0$ again

![[Verification 25_image_5.jpeg]]


==Inductive step==
It suffices to recall that [[w-regular]] languages are closed under [[Boolean Operations]] ($\lor,\land,\neg$) and [[Projection]].

__Remark:__ 
We may think of, starting from a formula of [[Monadic second order of one sucessor|S1S]], mapping it to [[Buechi automata]], and then going back to $S1S$, as a [[Normal form]] for [[Monadic second order of one sucessor|S1S]] formulas.

i.e. [[Buechi automata|Buechi-automaton]]s are kind of a normal form of [[Monadic second order of one sucessor|S1S]] formulas. As  when we translate the [[Buechi automata|Buechi-automaton]] back to [[Monadic second order of one sucessor|S1S]] we get it back in a very specific form.

$$\varphi \in S1S \rightarrow \mathcal{A} \rightarrow \overline{\varphi} \in S1S$$

[[Theorem 15|Buechis-theorem]] with small modifications, also holds in the finite case:

$\alpha \in A^*$ of length $k+1$
$\alpha = (\{0,...,k\},0,+1,<,\{P_i\}_{i=1,..n})$ 

__Reminder__
$\{P_i\}_{i=1,..n})$ is the set of all positions where the value of the word is 1 (there is one set for each of the $n$ bits)

We have to define what is $x+1$ for $x=k$ where $k$ is the last position. For instance we could say that $k+1=k$ problem solved.

We have to consider the empty word $\epsilon$. The standard assumptions are that $\epsilon$ satisfies all the universal statements ($\forall$) but it does not satisfy the existential ones ($\exists$).

Finally second order quantification is restricted to finite sets. Example: $\exists X...$ but $X$ is only allowed to take the form of finite sets.

> [!note] [[Theorem 16]] aka [[Theorem 15|Buechis-theorem]] on finite sets
> A language $L \subseteq A^*$ is a [[Regular Languages|Regular language]] $\iff$ it is definable in [[Monadic second order of one sucessor|S1S]] (In the finite setting)


==To summarize:==
1. We prove that Automatons can be expressed as [[Monadic second order of one sucessor|S1S]] formulas by expressing the rules for the initial condition, the [[Rule of Consequentiality]] and the [[Acceptance condition]]  (the steps that are needed for an [[Deterministic Finite State Automata|Automaton]]) in [[Monadic second order of one sucessor]] logic.
2. We prove stat [[Monadic second order of one sucessor|S1S]] and $S1S_0$ are equivalent
3. Then we focus on $S1S_0$ and its operations $SUCC$ and $\subseteq$  and express them as automatons. As $S1S_0$ formulas can be expressed in  [[Buechi automata|Buechi-automaton]]s, due to its equivalence to [[Monadic second order of one sucessor|S1S]] it means that also [[Monadic second order of one sucessor|S1S]] can be expressed as [[Buechi automata|Buechi-automaton]].

Some Remarks to the importance of this results:
The [[Theory]] [[Monadic second order of one sucessor|S1S]] is the set of [[Monadic second order of one sucessor|S1S]] [[Logical Sentence]]s which are true in the considered  $(\omega,0,+1,<)$. 

Examples:
[[Logical Sentence]] that is in the [[Theory]]:
$$\forall X \exists Y \forall x(x \in X \implies x\in Y)$$
[[Logical Sentence]] that is ==not in the [[Theory]] ==as it is not 
$$\forall X \exists y \forall x (x \in X \implies x < y)$$
Possible choice for when the formula is wrong is: $\omega$, the odd numbers, the even numbers (basically all infinite umbers)

The interpretation of the formula is that we need to find a element y (a number) that is greater than every number of the set $X$. If we choose $X$  as an unbounded set, for instance, the set of all Natural numbers $\omega$ we can not find a number that is bigger than all elements, as $X$ stretches out to infinity.

> [!note]
> $\omega$ is the set of [[Natural numbers]] $\mathbb{N}$

> [!note] [[Corollary 7]]
> The [[Theory]] of [[Monadic second order of one sucessor|S1S]] is [decidable](decideability.md).

In this case it means that we can decide if a [[Monadic second order of one sucessor|S1S]] formula is true or not.
Why can we decide? Because we can convert a [[Monadic second order of one sucessor|S1S]] formula to an input free  [[Buechi automata]] and in the [[Buechi automata]] the [[decideability]] problem is the [[emptyness problem]] which is decidable.


Sounds easy: Transfer [[Monadic second order of one sucessor|S1S]] to a [[input free automaton| input free]] [[Buechi automata]] and then find a way from the initial state to a end state that is in a loop. But the probem is the translation from [[Monadic second order of one sucessor|S1S]] to [[Buechi automata]], that is very complex.


Membership in the [[Theory]] of [[Monadic second order of one sucessor|S1S]] is [[elementary|non-elementary]].
Example:
$$\begin{align}
exp_0(n)&:=n\\
exp_{h+1}(n)&:= 2^{exp_h(n)}\end{align}$$
Whenever one increment by one, we have a exponential gap between the values.

$$\begin{align}
exp_0(n)&:=n\\
exp_{1}(n)&:= 2^{n}\\
exp_{2}(n)&:=2^{2^n}\\
...\\
exp_{h}(n)&:=2^{2^{2^{...^{2^{n}}}}}
\end{align}$$
In the last case we have $h$ occurrences of $2$. The height of the tower depends on $h$

Every time $h$ increases the tower gets higher and we change the function, not only the input value of the function. Exactly this is [[elementary| non elementary feature]]. We can not find a upper limit for the height of the tower (of the number of exponentials)

A problem is [[elementary|non-elementary]] when one is not able to find a bound to the tower of exponentials.

If one takes a [[Logical Sentence]] to prove the membership in [[Monadic second order of one sucessor|S1S]]  is not elementary.

On the other side if we have a [[Buechi automata]] $\mathcal{A}$ where we know that membership is [[logical equivalence|logically equivalent]] to the emptiness problem is decidable in [[P-Time|polynomial time]].

[[Theorem 15|Buechis-theorem]] says that we can transfer [[Monadic second order of one sucessor|S1S]] to [[Buechi automata]].

The problem is that the translation is possible but the size of the automaton is [[elementary|non-elementary]] meaning the size grows exponentially exponentially exponentially ....

Tools to translate the formulas are in fact not that bad (one powerful one is called MONA).

==Now lets show where the [[elementary|non-elementary]] feature come from?== 

Think of [[Monadic second order of one sucessor|S1S]] formulas as written as follows in [[Prenex Normal Form]], further we try to eliminate all $\forall$ by replacing them with a block starting with $\neg \exists$ then a lot of $\exists$ and then ending again with $\neg \exists$.


$$\exists \exists.... \underbrace{\forall \forall \forall \forall \forall \forall}_{\neg \exists \exists \exists ... \exists \exists \neg \exists} .....\exists ... \underbrace{\forall \forall}_{\neg \exists \exists...\exists \neg \exists}()$$

We have a exponential growth (the height of the exponential tower(the parameter $h$)) is given by the number of changes between the $\forall$ quantifier and the $\exists$ quantifier. If we have a sentence with a big size but no changes in quantifiers, the formula is easily translatable. The more changes in quantifiers ($\exists$ to $\forall$ and back and forth) we have the exponential tower growth.

==The fundamental parameter for the complexity of the sentence is the number of alternations of existential and universal quantifiers.==

As a matter of fact [[Buechi automata|Buechi]] did not consider [[Monadic second order of one sucessor|S1S]] but a slightly different form of [[Monadic second order of one sucessor|S1S]] called [[Monadic second order of one sucessor|WS1S]] by constraining the second order quantified variables to be interpreted over finite sets. 

 ==One can force this constraint on [[Monadic second order of one sucessor|S1S]]. Lets do it:==
$$X \rightarrow X= \emptyset \lor \exists (x \in X \land \forall y| x<y \implies y \not \in X)$$
 
This means that $X$ must be finite.

==expressiveness of [[Monadic second order of one sucessor|WS1S]]==
As we can express the constraint of [[Monadic second order of one sucessor|WS1S]] in normal [[Monadic second order of one sucessor|S1S]] it shows that [[Monadic second order of one sucessor|S1S]] is at least as expressive as [[Monadic second order of one sucessor|WS1S]].

==As a matter of fact [[Monadic second order of one sucessor|S1S]] is as expressive as [[Monadic second order of one sucessor|WS1S]].== (Not shown here, only one direction of the prove is shown)

| $S1S$                                         | $WS1S$                                              |
| --------------------------------------------- | --------------------------------------------------- |
| $W^W$ Infinte concatinations of infinte words | $\vec{W}$ infinite concatinations of finite objects |

 ---
 
26b

---
 
Is it possible to extend  [[Monadic second order of one sucessor|S1S]] with some predicates and still  preserving [[decideability]]? 

There are some such extensions. For instance:
- [[Monadic second order of one sucessor|S1S]] + [[unary operator|unary predicate]] "is  a power of 2"  and decidable
	$(\omega,0,+1,<,power)$
	$power$ is true on the elements of $2^n$ i.e. $power=\{1,4,9,...\}$

![](Verification%2025_image_6.png)


- [[Monadic second order of one sucessor|S1S]] + factorial is decidable
	$(\omega,0,+1,<,fact)$
	fact is true on the elements of $!n$ i.e. $fact=\{1,2,6,18...\}$

What happens if I add the function $2 \cdot x$? In this case the [[Theory]] becomes [undecidable](decideability.md)! This is enough to capture the entire arithmetic at [[FO - First order logic|FO]] and [[FO - First order logic|FO]] is undecidable.

Lets look at another extension, that preserves [[decideability]] is the following one: We can look at the natural numbers as a  [degenrate tree](tree.md). The degenerate tree we are looking at has the property that every node of the tree has only one successor (see left side of the image), which is equivalent to the natural numbers.

![](Verification%2025_image_7.png)

But we can extend it and transform this tree, to a binary tree where every node has two successors (right side of the tree), where we represent the nodes as binary numbers.

The [[Theory]] of the infinite binary tree is [[decideability|decidable]] and the theory of it is called [[The monadic second order theory of two successors]] aka [[The monadic second order theory of two successors|S2S]]. 

So the [[Monadic second order of one sucessor|S1S]] with only one successor could be looked at a special case of [[The monadic second order theory of two successors|S2S]].

What happens if we want more successors like 7 or 14. We can show that it can be encoded using the [[The monadic second order theory of two successors|S2S]] binary tree.

Interesting note: The theory is decidable not everything, i.e. we can say if something is part of the theory or not.

Additionally this two different kinds of thinking of computation find their way into two classes of [[temporal logic]]s which we will explore later.

1. [[linear temporal logic]]
	They look at a single line of computation like in the natural numbers (degenrate tree above)
2. [[Branching temporal logic]]
	 Here one can look at multiple computations at the same time, like in a binary tree

# 1 Results from [S1S](Monadic%20second%20order%20of%20one%20sucessor.md): [Determinization](Determinization.md)

To show [Determinization](Determinization.md) we first have to assume something without proving it before:
[Buechi automata](Buechi%20automata.md) are non deterministic. We also know that deterministic automata are much easier to deal with than non-deterministic automata. Unfortunately, ==deterministic [Buechi automata](Buechi%20automata.md) are less expressive than non-deterministic [Buechi automata](Buechi%20automata.md)==. 

>[!note] 
>Deterministic [Buechi automata](Buechi%20automata.md) are less expressive than non-deterministic [Buechi automata](Buechi%20automata.md).

So this is the first thing we will show now:
Deterministic [Buechi automata](Buechi%20automata.md) are less expressive than non-deterministic [Buechi automata](Buechi%20automata.md).

The second thing we will explore is why we only consider [Buechi automata](Buechi%20automata.md) where the deterministic and non-deterministic variants are differently expressive, while there are different automata where deterministic = non-deterministic. Why do we not use those to show our results?

## 1.1 Deterministic [Buechi automata](Buechi%20automata.md) [DBA](Buechi%20automata.md)

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

>[!Exercise]
>Prove that [DBA](Buechi%20automata.md) are closed under union and intersection.
>Tipp: The proof for [Intersection](Intersection.md) is simmilar to the proof for [NBA](Buechi%20automata.md).
>In the case of the Union one has to change a bit. Because in the classical proof one exploits non-determinism. One has to find a way to build a [NBA](Buechi%20automata.md) that recognizes the [Union](Union.md) of two languages recognized by a [NBA](Buechi%20automata.md).

## 1.2 Proposition

>[!proposition]
>A language $L \subseteq A^\omega$ is recognized by a [DBA](Buechi%20automata.md) if and only if ($\iff$) the language can be written as the [Vectorial closure](Vectorial%20closure.md) of $\omega$ i.e. $L=\overrightarrow{\omega}$ for some regular language $w \subseteq A^*$ 

### 1.2.1 Proof:
Let $$\mathcal{A}=\{Q,A,\delta,q_0,F\}$$ be a [DBA](Buechi%20automata.md) and let $$\mathcal{A'}=\{Q,A,\delta,q_0,F\}$$ be the corresponding [DFA](Deterministic%20Finite%20State%20Automata.md)

Let $w \subseteq A^*$ be the language recognized by $\mathcal{A'}$  which is: $w=L(A^*)$  $w$ is the language accepted by $A^*$.

We proof that $L(A)=\overrightarrow{w}$ 

First direction: (The infinite word is part of the vectorial closure of $w$)
By definition of acceptance condition of [Buechi automata](Buechi%20automata.md), Independt if deterministic or non-determinstic, and their deterministic nature of the Automation $\mathcal{A}$, we have that $A$ accepts $\alpha$ if and only if $(\iff)$ the computation of $A$ on $\alpha$ is sucessfull. That is $IN(\sigma) \cup F = \emptyset$. Lets paint it:

![](Verification%2025_image_8.png)
$\alpha$ is the infinite word accepted by $\mathcal{A}$. As it is accepted we pass through a final state $q_F$ infinitely many times.

When we consider the start of the sentence to each of the $q_F$'s as a finite word, we get words that are accepted by the [DFA](Deterministic%20Finite%20State%20Automata.md) $\mathcal{A'}$. As we pass through $q_F$ infinitely may times we have infinitely many prefixes inside $\alpha$ that are accepted by $A$.

This allows us to conclude that $\alpha$ belongs to the vectorial closure of $w$ i.e. $\overrightarrow{w}$. [Vectorial closure](Vectorial%20closure.md)

Other direction:

Let us assume that $\alpha \in \overrightarrow{w}$ .
For all [prefix](prefix.md)es of $\alpha$ belonging to $w$ (which is equivalent to the language accepted by $\mathcal{A'}$ i.e. $L(\mathcal{A}')$) the successful computation of $\mathcal{A'}$ on them can be viewed as a prefix of the unique computation of the [DBA](Buechi%20automata.md) of $\mathcal{A}$ on $\alpha$.

This means as shown in the image below:
one valid word is from $q_0$ to $q_F$ (lets call this $q'$) then from $q_0$ to $q_F$ to the next occurrence of $q_F$ (lets call this $q''$). Meaning that we have infinitely many words accepted by $\mathcal{A'}$.

![](Verification%2025_image_9.png)



One could say, that maybe the final states vary, i.e. once it is $q_F$ then $q_F'$ and this would change the game, but we can ignore all other final states as $F$ is finite meaning to have infinite occurrences of elements of $F$ at least one has to appear infinitely many times. We focus on this one, we name it $q_F$.

Since by hypothesis $IN(\sigma) \cap F \neq \emptyset$ it follows that the $w \text{-word}$ $\alpha$  is also accepted by $\mathcal{A}$ i.e. $\alpha \in L(\mathcal{A})$.
$\square$ 

