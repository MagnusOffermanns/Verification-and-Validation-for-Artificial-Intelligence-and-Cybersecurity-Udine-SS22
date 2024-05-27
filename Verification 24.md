# 1 [[Monadic second order of one sucessor|S1S]]
==Definition== of [[Monadic second order of one sucessor|S1S]] over an Alphabet $A$: $S1S_A$ 
Let $A$ be a finite alphabet of symbols. The language of $S1S$ over $A$ is defined as follows:

- __terms__ are obtained from the constant $0$ and [[FO - First order logic|FO]] variables $x,y,z$ by possibly applying the (unary) function $+1$ (successor) (for instance: $\phi,x,z,x+1$)
- __atomic formulas__: which are of the following form: 
	- $t_1=t_2$
	- $t_1<t_2$
	- $t_1 \in X$ ($X$ is a second order variable)
	- $t_1 \in Q_a$ with $a \in A$ ($Q_a$ is a unary predicate, one for each $a \in A$)

Formulas of $S1S_A$ are obtained from atomic ones, by possibly applying Boolean connectives ($\lor,\land,\neg$) and Quantifiers $\exists, \forall$ on both kinds of variable.

Example: $\exists x, \forall X$ are both admissible in this language. 

![[Verification 24_image_1.jpeg]]

$A=\{a,b,c\}$
The interpretation of $Q_a$is the positions where there is $a$ occurring in $\alpha$. i.e.:
$$Q_a=\{0,3,4,6....\},\quad Q_b=\{2,7,...\}, \quad Q_c=\{1,5,...\}$$

One can represent a [[omega-words|w-word]] using the Q-sets.

==Reminder:== What is the difference between open and closed formulas?

- __[[Open fomulas]]__ 
	Is a formula in which there are some free variables example: $\forall x (y<x)$ 
	$y$ is a [[free variables|free variable]]
- [[Closed Formulas]]
	Is a formula in which there a no [[free variables]] example: $\forall x \exists y (y<x)$

## 1.1 Remark
As a matter of fact, both the constant 0 and the ordering relation $<$ are definable in $S1S_A$ (And are redundant).

As for 0, we can replace $x=0$ by: $\forall y (x<y \lor x=y)$
Can we define it without the ordering relation $<$? Yes like this $\neg \exists y (y+1=x)$

We will use the zero, but as just shown it can be removed, we use it just out of lazynes to be more concise.

As for the ordering relation $<$ it is a bit more complicated.
First we show that the successor relation can be defined only using $<$.
$$x=y+1 \equiv y<x \land \neg \exists z (y<z \land z < x )$$
$y<x$ states that y is smaller than x
$\neg \exists z (y<z \land z < x)$ states that there should be no element between $y$ and $x$

Summarizing: $+1$ and $<$ are first order definable (we only use tools from [[FO - First order logic|FO]])

We show how to define ordering $<$ in terms of successor (second order definable)

$x<y$ can be rewritten as:
$$\forall X (x+1 \in X \land \forall z (z \in X \implies z+1 \in X )) \implies y \in X $$

![[Verification 24_image_2.jpeg|600]]

Why do we use $\forall X$ and not $\exists A$ ?

![[Verification 24_image_3.jpeg|600]]


## 1.2 What does Monadic mean?
==Monadic is a synonym for unary==

The only predicates we can use in [[Monadic second order of one sucessor|S1S]] apart from = are [[unary operator|unary predicates]].

==Remark:== The [[Ordering relation]]  $<$ is not definable  in terms of the [[successor relation]].

---
brake

---

## 1.3 How to use formulas of [[Monadic second order of one sucessor|S1S]]A to define Languages?
A model-theoretic interpretation of [[omega-words|w-word]]s can be given as follows:

Let $\alpha \in A^w$ it model theoretic interpretation is: 
$$\alpha = (\omega,0,+1,<,\{Q_a\}_{a \in A}\}$$
$\omega:$ is the set of Natural Numbers $\mathbb{N}$ 
$Q_a=\{i \in w : \alpha(i)=a \}$

Given a sentence $\phi$ of [[Monadic second order of one sucessor|S1S]]a, the language defined by $\phi$ is:
$L(\phi)=\{ \alpha \in A^w: \alpha \models \phi\}$ 
This means that this are all [[omega-words|w-word]]s $\alpha$ that make $\phi$ true

==Examples:==
Example 1:
Let $L$ be the language over $A=\{a,b,c\}$ that includes all and only those [[omega-words|w-word]] such that every occurrence of the symbol $a$  is followed by an occurrence of the symbol $b$. This does not mean that a $b$ has to be the successive symbol of $a$ but at some point in the future a $b$ will occur (this is a way to encode [[Accessibility property|Accessibility]]).

$$\forall x (x \in Q_a) \implies \exists y (y \in Q_b \land x<y)$$

Example 2:
Let $A=\{a,b,c\}$ where between any pair of consecutive occurrences of $a$ there is a even number of occurrences of the  letter $b$ and/or $c$.

$$\forall x \forall y (x \in Q_a \land y \in Q_a \land x < y \land \neg \exists z (z \in Q_a  \land x<z<y) ) \implies \exists X (x \in X \land \forall z (z \in X \implies z+1 \not \in X) \land y \not \in X )$$

- $\forall x \forall y (x \in Q_a \land y \in Q_a \land x < y \land \neg \exists z (z \in Q_a  \land x<z<y) )$  This part is saying that if there are two symbols of the same kind ($a$) there is no third symbol of the same kind (a) between them ($z$).
- $\exists X (x \in X \land \forall z (z \in X \implies z+1 \not \in X) \land y \not \in X )$ This means that we can create a set $X$ so that once symbol is in the set, and the following is not in the set, denoting the allowed positions of $a$ (every other position), lastly the following consecutive $y$ needs to be in the set of even positions ($X$) and not in the set of  uneven positions $\overline{X}$

Visually :
![[Verification 24_image_4.jpeg|600]]

![[Verification 24_image_5.jpeg|600]]



# 2 Alphabet less  Formulas
Currently we are defining [[Deterministic Finite State Automata|Automata]] on a certain Alphabet. We want to show that we can also define them on arbitrary alphabets. We want to remove the dependency of A.

We want to go from $S1S_A \to S1S$.

To this end is it sufficient to replace $A$ by $\{0,1\}^n$, where $n= log_2(|A|)$ 

Example:
- $A=\{a,b,c\} \to n=2$
We need enough 0 to encode the alphabet.

Lets consider a [[omega-words|w-word]] $\alpha$ how can we rewrite it in the new alphabet?

lets encode $a=(0,0),b=(0,1),c=(1,0)$

![[Verification 24_image_6.jpeg|600]]

The interpretation of $X_1$ that captures $\alpha$ is: $int(X_1)=\{3\}$
The interpretation of $X_2$ that captures $\alpha$ is: $int(X_2)=\{1,2\}$

We replace the predicates $Q_a$, $Q_b,Q_c$ with a set of second order variables $X_1,X_2...,X_n$ and each [[omega-words|w-word]] $\alpha$ will be represented by the following model-theoretic interpretation:

$$\alpha=(w,0,+1,<,\{P_i\}_{i=1,2,3..n})$$

$P_i$ is the equivalent of $X_i$ in the image above i.e.
$P_i=\{j \in \omega: (\alpha(j))_i=1\}$

for $j=1,2,...n$

It can be shown that each of the sentences of $S1S_A$ can be replaced by an equivalent formula of the form $\psi(X_1,X_2,...X_n)$ 


Given a [[Monadic second order of one sucessor|S1S]] formula $\phi(X_1,X_2,...,X_n)$ the language defined by $\phi(X_1,X_2,...,X_n)$ is $L(\phi)=\{\alpha \in (\{ 0,1\}^n)^w: \alpha \models \phi(X_1,X_2,...,X_n)\}$  

An  [[w-regular|w-language]] $L \subseteq A^w$ is definable if $L=L(\phi)$ for some [[Monadic second order of one sucessor|S1S]] formula $\phi$.

> [!note] [[Lemma 14]] (Closure under projection)
> Let $\psi(X_1,X_2,...,X_{i-1},X_{i+1},X_n)$ be the [[Monadic second order of one sucessor|S1S]] formula: $\exists X_i: \phi(X_1,X_2,...,X_{i-1},X_i,X_{i+1},X_n)$. If $L(\phi)$ is [[w-regular]], then $L(\psi)$ is also [[w-regular]] as well.

 ![[Verification 24_image_7.jpeg|600]]

==What does this mean? What is even Projection?==
[[Projection]] is the same as in Databases.

We have a automaton which is [[w-regular]] and has the components $X_0$ till $X_n$. If we now remove one of the components e.g. $X_i$ the resulting [[Deterministic Finite State Automata|Automaton]] without $X_i$ (e.g. $\{X_0....X_n\}-X_i$) is still [[w-regular]].

Lets go to an extreme and remove all components resulting in not having any components, then we use that we have a [[Buechi automata|Buechi-automaton]] which is non deterministic. Then the automaton is a special automaton where the edges do not have labels we call this: [[input free automaton]]. This is the formula equivalence of a [[Logical Sentence]].

---
start 25a

---




