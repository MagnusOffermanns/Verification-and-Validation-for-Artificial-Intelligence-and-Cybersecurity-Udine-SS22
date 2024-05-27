In $A_5$ we see $G(p)$ the universal condition (p is always true from a certain timepoint $t$). When applying the alpha Rule $R_\alpha$ also $p$ and $X(G(p))$ need  to be part of the State $A_5$ aka Atom 5.

All formulas of All States need to be consistent i.e. they must be somehow [Satisfiable](Satisfiability.md) that means that for instance $p \land \neg p$ will not be part of any atom as it is not **satisfiable**.

How do we handle the successor relation: If we have the next operator $X$, the argument of the Next operator needs to be in the next state i.e. 
$X(G(p))$ in the next state it needs to have $G(p)$.


The problem is the existential conditions: $R_\beta$. By construction we can not be sure that all existential conditions are satisfied [satisfiable](Satisfiability.md).

 The initial state $A_0$ needs to be true at time point $[0]$ i.e. $\sigma$ must be a model of our formula $\varphi$. Therefore also at the counterexample we can only start in $A_7$ as it is the only one containing $\varphi$ i.e. which models $\varphi$


summary:
![](Verification%2032_image_1.png)

$A_7^\omega$ is not an [Induced Path](Induced%20Path.md) as according to the $R_\beta$ it must contain $X(F(p))$ which it does not.

![](Verification%2032_image_2.png)

![](Verification%2032_image_3.png)

If we have a promising formula (one of the above) we have two ways to fullfill the promise. We need to have infinitely many times either the one or the other.
1. the formula will be true at some point in the formula or
2. we negate the formula that [Promises](Promise.md) at some point in the future

## 0.1 Fullfilling atoms and fullfilling paths

### 0.1.1 fullfilling Atoms -> fullfiling promises
>[!Note] Fullfilling Atoms
> An [[Atom]] $A$ fullfills a formula $\psi$, that [Promises](Promise.md) $r$, if $\neg \psi \in A$ or $r \in A$

### 0.1.2 Fullfilling paths

>[!Note] Fullfilling path
>A path $\pi =A_0,A_1,\dots$ in a [Tableaux](Tableaux.md) $T_\varphi$ is fullfilling if for every promising formular $\psi \in \phi_\varphi$ (formula in the [Closure](Closure.md)), $\pi$ contains infinitely many atoms $A_j$ which fullfill $\psi$ (that is either $\neg \psi \in A_j$ or $r \in A_j$ )

==An example:==
![](Verification%2032_image_4.png)
If we look at the path $A_7^\omega$ we see that it is not a good atom as it is not ==fullfilling path==
It contains $F(\neg p)$ but it does not contain $\neg p$ nor $\neg F(\neg p)$.


==Additional Examples:==

Example 1:

![](Verification%2032_image_5.png)

The path:
![](Verification%2032_image_6.png)
We stay forever in $A_2$

Why is it not good for validity checking of $\varphi$? It only contains $\neg \varphi$ in the initial state i.e. $A_2$!

Example 2:
![](Verification%2032_image_7.png)

$A_3$ is not fullfilling as it contains the [Promise](Promise.md) $F(\neg p)$ but it does not contain $\neg p$. But we have $A_2$ that is fullfilling (as already shown in example 1), and as $A_2$ is occuring infinitely many times, the path is fullfilling.

Why is it not good for validity checking of $\varphi$? It only contains $\neg \varphi$ in the initial state i.e. $A_2$!


==Example 3: ==
![](Verification%2032_image_8.png)

$A_4$ promises $F(\neg p)$ so to fullfill the promise $A_5$ either has to contain $\neg p$ or the negation of the promising formula which is $\neg F(\neg p)$. And indeed it contains the formula $\neg F(\neg p)$ making it a fulfilling path.

Why is it not good for validity checking of $\varphi$? It only contains $\neg \varphi$ in the initial state i.e. $A_4$!

Only $A_7$ contains $\varphi$ making it the only reasonable initial state.


>[!Note] Models induce fullfilling paths
>If $\phi_\sigma=A_0,A_1,\dots$ is a path induced by a model $\sigma$ then $\pi_\sigma$ is fullfilling.

![](Verification%2032_image_9.png)


Now we have to proof that if there is a fullfilling then there exists a corresponding model.
>[!Note] Proposition
>If $\pi=A_0,A_1,\dots$ is a fullfilling path in the [Tableaux](Tableaux.md) $T) \varphi$ then there exists a model $\sigma$ inducing $\pi$, that is $\pi=\pi_\sigma$ and for every $\psi \in \phi_\varphi$ (formula in the closure) and every $j \ge 0, (\sigma,j) \Vdash \phi$ if and only if ($\iff$ ) $\phi \in A_j$ 

![](Verification%2032_image_10.png)

![](Verification%2032_image_11.png)

---
32 b

---

### 0.1.3 Main Result:
>[!Note] Main Result
>A formula $\varphi$ is [satisfiable](Satisfiability.md) if and only if the [Tableaux](Tableaux.md) $T_\varphi$ contains a fulfilling path $\pi=A_0,A_1,\dots$, **additionally** $\varphi$ must be part of the state $A_0$.

![](Verification%2032_image_12.png)

Now we need to find a way to check weather the a  path is fullfilling. As there are infinitely many infinite paths, this is challenging.

## 0.2 Applications
==Example 1:==
![](Verification%2032_image_13.png)

==Example 2:==
Is $\neg \varphi: \neg G(p) \lor \neg F(\neg p))$ satisfiable?
We remember the [Tableaux](Tableaux.md) for $T_{\neg \varphi}$ is the same as $T_\varphi$.

Now we only need to find a fullfilling path!

1. We need to find a initial state $B_0$ that contains $\neg \varphi$ i.e. ($\neg \varphi \in B_0$). As can be seen all states except $A_7$ are good initial states (only following this requirement)
![](Verification%2032_image_14.png)

Then we need to find a [[fullfilling path]]:
One example would be $A_5^\omega$.

It is fullfilling as it contains the negation of the only promising formula in the [Closure](Closure.md) $\phi_\varphi$, which is $F(\neg p)$  i.e. $\neg F(\neg p)$.


## 0.3 How do we check for the existence of [fullfilling paths](fullfilling%20path.md)?

Therefore we introduce the notion of the [strongly connected](strongly%20connected.md) subgraph. We already know the notion of [strongly connected](strongly%20connected.md) from network science.

>[!Note] Strongly connected subgraph.
>A subgraph $S \subseteq T_\varphi$ is a strongly connected subgraph if for every pair of [Atoms](Atom.md) $A,B \in S$ there exists a path from $A$ to $B$ that only passes through atoms of $S$

The maximum number of SCS in a [Tableaux](Tableaux.md) is equal to the number of nodes, where each SCS only contains a single Atom.

For instance in our [Tableaux](Tableaux.md) we have the following seven SCS:
 
1. $A_2,A_3$
2. $A_0$
3. $A_1$
4. $A_4$
5. $A_5$
6. $A_6$
7. $A_7$

Counter example: $A_0,A_1$ is not a ==SCS== as there is a path from  $A_0 \rightarrow A_1$ but no way from $A_1$ to $A_0$

![](Verification%2032_image_15.png)

How an we guarantee now a fullfilling path from such a graph?

We want to define a easy check:
- Is there  for every [Promiseing](Promise.md) formula, an Atom that fullfills the promise?

In our example we only have one promising formula $F(\neg p)$. $A_3$ does not fullfill the promise, but $A_2$ has it. As $A_2,A_3$ is a SCS, we have a fullfilling path.

Also $A_5$ is a fullfilling non-transient SCS

>[!Attention] Why is $A_1$ a not fullfilling non transien SCS?
Also $A_1$ is a non fullfillling non transient SCS.
We have $\neg G(p)$ where $G(p)$ can be written as: $\neg F(\neg p)$ i.e. $\neg G(p)\equiv F(\neg p)$ i.e. it promises $\neg p$. Unfortunately $A_1$ only contains $p$ meaning the promise is not held :(


>[!Note] Definition ==fullfilling SCS==
>A non transient **SCS** is **fullfilling** if every formula $\psi$ in the closure $\phi_\varphi$ (i.e. $\psi \in \phi_\varphi$) that [Promises](Promise.md) $r$ is fullfilled by some [Atom](Atom.md) $A \in S$ (i.e. either $\neg \psi$ or $r \in A$ or both) where ** transient SCS** is an SCS consisting of a single node not connected to itself.

Examples of transient **SCS**: $A_1$ or $A_4$ or $A_6$
Examples of non-transient **SCS** (because they have a self loop): $A_1$ or $A_5$ or $A_7$

Solution to our ==Example==
![](Verification%2032_image_16.png)

>[!Note] $\varphi$-reachable
A [[VV Strongly connected subgraph]] S is $\varphi$-reachable [VV SCS](VV%20Strongly%20connected%20subgraph.md) if there exists a finite path $B_0,B_1,\dots,B_k$ such that $\varphi \in B_0$ and $B_k \in S$

>[!Note] Proposition
>A [Tableaux](Tableaux.md) $T_\varphi$ contains a fullfilling path starting at an $\varphi$-atom if and only if ($\iff$) $T_\varphi$ contains a $\varphi$-reachable fullfilling **SCS**

>[!Note] [[Corollary 8]]
>A formula $\varphi$ is satisfiable if and only if the [Tableaux](Tableaux.md) $T_\varphi$ contains a $\varphi$-reachable fullfilling SCS