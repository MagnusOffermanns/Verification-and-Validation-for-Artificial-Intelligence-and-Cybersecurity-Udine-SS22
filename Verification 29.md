==Contiinuation 29b 18:10==

# 1 [temporal logic](temporal%20logic.md)

Overview:
1. classification
2. [linear time temporal logic](temporal%20logic.md)
3. [branching time temporal logic](temporal%20logic.md)
4. [Model-checking](Model-checking.md)

## 1.1 [linear time temporal logic](temporal%20logic.md)

### 1.1.1 [[Modal logic]]
Is a form of logic that takes the situation in consideration. That means that a formula can be True in one situation and false in another situation. It takes the context into consideration. In [temporal logic](temporal%20logic.md) a formula is either True or False, it is globally valid.


$\square$ -> always true
$\diamondsuit$ -> necessarily true (sometimes)

## 1.2 Propositional Linear Temporal Logic
### 1.2.1 Syntax
- $P,Q$ Propositional letters $AP$
- $\neg,\land$ Porpositional connectives
- $X$: Next, $U$: until temporal connective
	- $X$: what does the Next operator mean?
		 $X(p)[t]$ (i.e. $X(p)$ at time $t$)is true depending on the state of $p$ in the next time step : If $p[t+1]=False$ -> $X(p)[t]=False$. If  $p[t+1]=True$ -> $X(p)[t]=False$. $X(p)$ does only depend on the value of $p$ in the future state, it does not depend on the state of $p$ at timepoint $t$ i.e. $p[t]$.
	- $U$: what does the until operator mean?
		$U$ has two arguments we write it like this  $(p)U(q)$.
		$(p)U(q)$ is only true if $p$ is true until $q$ is true. If $p$ ever goes False before $q$ becomes true, the statement is false. The statement is also only true if $q$ ever becomes true in the future. If $q$ stays $False$ until infinity $(p)U(q)[t]$ also stays False.
- Formulae: $P,p\land q, \neg p, Xp,pUq$

Below one sees the relation of $X(p)[t]$ to the state of $p$ at time $[t+1]$. $X(p)[t]$ is only true if $p$ is true at $t+1$ i.e $p[t+1]$.

![](tmp1708678234020_temporal%20logic_image_1.png)

$pUq$ ist nur wahr wenn $p$ immer True ist bis $Q$ das erste mal True wird
![](tmp1708879099593_temporal%20logic_image_2.png)


Lets do an ==Example:==
We want to define a operator that is only true if $p$ gets true sometimes in the future we denote this as $F(p)$.
$F(p)$ defined using the $U$ connective:
$$F(p) \equiv (True)U(p)$$

Another example:
We want to denote a operator that is true if a variable $p$ is always true in the future the shortform for this is $G(P)$
$$G(p) \equiv \neg F(\neg p)$$

Das kann gelesen werden als:
- $F(\neg p)$: $p$ wird irgendwann in der zukunft negativ
- $\neg F(\neg p)$: $p$ wird irgendwann in der zukunft nicht negativ i.e. p wird positiv i.e. bleibt positiv

This means that we can also express $G$ in the terms of $F$.
$$F(p) \equiv \neg G(\neg p)$$

>[!Note]
> We can define $F$ and $G$ over $U$, but not the other way around we can not define $U$ using $F$ and/or $G$



