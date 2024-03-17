---
aliases:
  - S1S
  - S1S_0
  - WS1S
  - S1SA
---

# 1 $S1S_A$
Let $A$ be a finite alphabet of symbols. The language of $S1S$ over $A$ is defined as follows:

- __terms__ are obtained from the constant $0$ and [[FO - First order logic|FO]] variables $x,y,z$ by possibly applying the (unary) function $+1$ (successor) (for instance: $\phi,x,z,x+1$)
- __atomic formulas__: which are of the following form: 
	- $t_1=t_2$
	- $t_1<t_2$
	- $t_1 \in X$ (X is a second order variable)
	- $t_1 \in Q_a$ with $a \in A$ ($Q_a$ is a unary predicate, one for each $a \in A$)

Quantifiers can only be applied on sets for instance: $X$ or $Y$

Example formula:

$$\forall X (x+1 \in X \land \forall z (z \in X \implies z+1 \in X )) \implies y \in X $$

# 2 $S1S_0$
$S1S_0$ formulas are a special form of [[Monadic second order of one sucessor|S1S]] formulas that  only admit second order variables and atomic formulas of the forms:
- $X \subseteq Y$
- $SUCC(X,Y)$ where $X=\{x\}$ and $Y=\{y\}$ and $y=x+1$

# 3 Weak $S1S$ alias $WS1S$
Is like S1S but second order quantified variables can only be interpreted in finite sets.

As a matter of fact [[Monadic second order of one sucessor|S1S]] is as expressive as [[Monadic second order of one sucessor|WS1S]]. Proven in [[Verification 25]] it is [Theorem 20](Theorem%2020.md).


# 4 Relationship to state automata

![](Monadic%20second%20order%20of%20one%20sucessor_image_1.png)