>[!Attention]
>I mixed up the signs for $G(p)$ and $F(p)$ up as he is using three notations in the class  one has to go over the individual drawings and translate them form $\square$ and $\bigcirc$ to normal $F$ and $G$ notation.

Lets do an example of the using the decision procedure from [Verification 32](Verification%2032.md).

We revisit the formula from before $\neg \varphi: \neg G(p)\lor \neg F(\neg p)$

Lets also revisit the [Tableaux](Tableaux.md) from before and look at the [VV Strongly connected subgraph](VV%20Strongly%20connected%20subgraph.md) $S=\{A_2,A_3\}$.

$S$ is $\neg \varphi$-reachable fullfilling [VV SCS](VV%20Strongly%20connected%20subgraph.md) because:
$(A_2,A_3)^\omega: A_2,A_3,A_2,\dots$

and $\neg \varphi \in A_2$ (and also $\neg \in A_3$ but only need it in one of the two states)

Hence $\neg \varphi$ is satisfiable.
model is $(<p: False>,<p:True>)^\omega$

We read this from the value of $p$ in the respective Atom i.e. $\neg p \in A_2$ and  $p \in A_3$.

![](Verification%2033_image_1.png)


We can also improve the method a bit. Therefore we introduce [maximal strongly connected subgraphs](VV%20Strongly%20connected%20subgraph.md)

>[!note] [Maximal strongly connected subgraph](VV%20Strongly%20connected%20subgraph.md)
>An [VV SCS](VV%20Strongly%20connected%20subgraph.md) is a [Maximal strongly connected subgraph](VV%20Strongly%20connected%20subgraph.md) if it is not contained in any larger [VV SCS](VV%20Strongly%20connected%20subgraph.md) (remember that there exist at most as many [MSCS](VV%20Strongly%20connected%20subgraph.md)) as there are Atoms in the [Tableaux](Tableaux.md) i.e. $|T_\varphi|$

For example $A_2$ is not a [VV MSCS](VV%20Strongly%20connected%20subgraph.md) as it is contained in the [VV SCS](VV%20Strongly%20connected%20subgraph.md) $\{A_2,A_3\}$.

$\{A_2,A_3\}$ on the other hand is a [VV MSCS](VV%20Strongly%20connected%20subgraph.md) as it is not contained in another bigger subgraph.

Lets rewrite the initial proposition :

>[!Note] Proposition
>A Formula $\varphi$ is satisfiable if and only if the [Tableaux](Tableaux.md) $T_\varphi$ contains a $\varphi$-reachable fulfilling [MSCS](VV%20Strongly%20connected%20subgraph.md) (As a matter of fact we can preliminarily remove) all atoms which are not reachable from a $\varphi$-atom. 

Lets look at the example $\varphi: G(p) \land F(\neg p)$ and we remove all atoms that are not a $\varphi$-atom. We see that the resulting pruned graph only includes $A_7$.

The only [VV MSCS](VV%20Strongly%20connected%20subgraph.md) is $\{A_7\}$ and as this one is not fullfilling (it does not full fill the promise ($F(\neg p)$)) one can easily see that $\varphi$ is not satisfiable.

Lets look at the negation of $\varphi$ i.e. $\neg \varphi$:
The pruning does not remove any nodes as all nodes are reachable from a $\varphi$-Atom.

![](Verification%2033_image_2.png)

![](Verification%2033_image_3.png)


>[!Note] terminal MSCS
>An MSCS $S$ is terminal if there are no edges leading from atoms of $S$ to atoms outside of $S$

Examples:
$\{A_7\}$ and $\{A_5\}$ are terminal [MSCS](VV%20Strongly%20connected%20subgraph.md) while $\{A_6\}$ and $\{A_2,A_3\}$ are not.

One can prune [Atoms](Atom.md) from the [Tableaux](Tableaux.md) $T_\varphi$ if:
- which are not reachable from  a $\varphi$-atom.
- any [terminal MSCS](VV%20Strongly%20connected%20subgraph.md) which are not [fullfilling](fullfilling%20path.md).


## 0.1 How can we check [Validity](Validity.md) of $\varphi$?
To check the [Validity](Validity.md) of a formula we do a [Satisfiability](Satisfiability.md) check to the negation of the formula i.e. $\neg \varphi$. If $\neg \varphi$ is [satisfiable](Satisfiability.md), $\varphi$ is not [Valid](Validity.md).

if $\neg \varphi$ is not satisfiable, $\varphi$ is valid.



# 1 Introduction to [Model-checking](Model-checking.md) in [LTL](temporal%20logic.md).

Unlike simulation and testing techniques, formal verification conducts an exhaustive exploration of all possible behaviors of a system.

The use of theorem proves, term rewriting systems, and proof checkers in formal verification: they are time consuming and they often require a great deal of manual intervention (Temporal logic) model checking: an alternative verification technique developed independently by Clarke and Emerson in USA and by Queille and Sifakis in France at the beginning of the ’80s.

Specifications are expressed as formulae in a propositional temporal logic to be checked against state-transition systems (is the transition system a model of the specification?) by using efficient search procedures.

## 1.1 The distinctive features of [Model-checking](Model-checking.md)

The method of [Model-checking](Model-checking.md): a desired property of the system is verified over a given system (the model) through an exhaustive (explicit or implicit) enumeration of all the states reachable by the system and the behaviors that traverse through them 

Distinctive features of model checking:

- It is fully automatic
-  When the design fails to satisfy a given property, a counterexample is produced that exhibits a behavior which falsifies the property (useful insight to understand the reason for the failure and clues for fixing the problem)


>[!Note] What was the first systems that were investigated for [Model-checking](Model-checking.md)?
>The first systems investigated were [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) systems by a researcher called **Church**.
> If you have a system that can be described  by a [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula, one can syntesize an Automaton implementing the formula.


==We will learn this method in this class==

 >[!Note] What is [Model-checking](Model-checking.md)?
 A specification is a specification of a property in the form of a formula (for instance a [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula). Then we have a model of a system, in [Model-checking](Model-checking.md) we verify if all computations of a system are models of the formula (set the formula to $True$).

---
33b

---

## 1.2 [Model-checking](Model-checking.md)

In its original form, model checking is a simple (and very successful) method to decide the relation:

$$M,s \models \phi$$

Where $M$ is a [temporal structure](Kripke%20structure.md) / [[Kripke structure]] (set of states plus accessibility relation), $s$ is a designated state in $M$, and $\phi$ is a
formula of some temporal logic
Format of Kripke structures (over $P_1 ,\dots, P_n$ )


$M = (S, R, L)$

Where $S$ is the state set, $R \subseteq S \times S$ is the transition relation, and $L: S \rightarrow 2^{\{P_1, \dots, P_n\}}$  is the labeling function

The labeling function translates each state into one of the proposition letters ($P_1, \dots, P_n$)


## 1.3 [LTL](temporal%20logic.md)

We have already introduced [LTL](temporal%20logic.md) in the previous letters:

==Example:==
$$G(P_1 \rightarrow X((\neg P_2)U(P_1)))$$
This could be read in natural language as:
"after any time where $P_1$ holds, $P_2$ is false until $P_1$ holds again"

How can we now apply [Model-checking](Model-checking.md)?

We could [Model-check](Model-checking.md) the formula by writing:
$M,s \models \phi \iff \text{each path } \varPi=s,s_1,s_2,\dots$
$\text{ through } M \text{ satisfies } \phi$ 

When we use branching [LTL](temporal%20logic.md) we write it as $M$ satisfies $A\phi$ in short)

## 1.4 [Model-checking](Model-checking.md) in [LTL](temporal%20logic.md)
First [Model-checking](Model-checking.md) algorithm was introduced by Vardi and Wolper.

Given the structure  $(M, s)$ and the [LTL](temporal%20logic.md) formula $phi$, construct a Büchi automaton $A$ which accepts those paths $\Pi=s,s_1,s_2$ through $M$  which violate $\phi$
$$A=A_{(M,s)} \times A_{\neg \phi}$$

We check for non-emptiness of the Language of A i.e.  $L(A)$ where $L(A)$ is the set of bug scenarios.

**Complexity of model-chcking for LTL**: [P-Space](P-Space.md)-complete (same complexity as [Satisfiability](Satisfiability.md) for [LTL](temporal%20logic.md))

It is linear in $|M|(=|S|+|R|)$ i.e. the [Tableaux](Tableaux.md) but when we have to tranform it to a formula or from a formula to a [Tableaux](Tableaux.md) there transformation might have exponential complexity.


## 1.5 A solution for [Model-checking](Model-checking.md) for [LTL](temporal%20logic.md) by Manna and Pnueli

What is the idea:
We start with a [Tableaux](Tableaux.md) for the negation of the formula i.e. $\neg \phi$. 
Then we suppose that we have a graph that describes the behavior of the system. Then we put them together and do a [Cartesian Product](Cartesian%20Product). The we look in the resulting graph for a path that starts from an initial state that contains $\neg \phi$ (i.e. the formula we want to check). Then we want to find a path that is both [fullfilling](fullfilling%20path.md) for the formula and the transition system.

  >[!Note] Why do we check for the [Satisfiability](Satisfiability.md) of $\neg \phi$?
  >When $\neg \phi$ is true, that means that $\phi$ is false in this case, that means that our formula $\phi$ is not a model i.e. the [Model-checking](Model-checking.md) fails or $\phi$.
  
## 1.6 P-[Validity](Validity.md) and P-[Satisfiability](Satisfiability.md) problems (of $\varphi$)

#### 1.6.1.1 P-[Validity](Validity.md) problem (of φ)
Main question: given a finite-state program P and a formula $\varphi$, is $\varphi$ P-valid, that is, do all P-computations satisfy $\varphi$?
#### 1.6.1.2 P-[Satisfiability](Satisfiability.md) problem (of $\varphi$)
Main question: given a finite-state program P and a formula $\varphi$, is there a P-computation which satisfies $\varphi$?

To determine whether  is P-valid, it suffices to employ an algorithm for deciding if there is a P-computation which satisfied $\neg \varphi$.

The algorithm for solving the P-satisfiability of $\varphi$, makes use of the [Tableaux](Tableaux.md) for $\varphi$ i.e. $T_\varphi$.

### 1.6.2 Basic definitions

- $state(A):$ For each [Atom](Atom.md) $A$, let $state(A)$ be the conjunction of all [local formulas](local%20formula.md) in $A$ (by $R_{sat}$ , $state(A)$ must be [satisfiable](Satisfiability.md)).

- [consistent](VV%20consistent.md): Atom $A$ is [consistent](VV%20consistent.md) with state $s$ if $s \models state(A)$, that is, all state-formulas in $A$ are [satisfiable](Satisfiability.md) by $s$.
	Example: Lets suppose the onlh [local formula](local%20formula.md) in an Atom is the proposition letter $p$, we say that a certain state $s$ is [consistent](VV%20consistent.md) with an [Atom](Atom.md). When the state $s$ makes all local formulas $True$ . In our case this is only the formula $p$.

- [trail](trail.md): Let $\pi: A_1,A_2,\dots$ be a path in $T_\varphi$ and let $\sigma: s_0,s_1,s_2,\dots$ be a computation of $P$. $\theta$ is a [[trail]] of $T_\varphi$ over $\sigma$ if $A_j$ is [consistent](VV%20consistent.md) with $s_j$ , for all $j \ge 0$.

- $\sigma(A):$ For each atom $A \in T_\varphi$ , $\delta(A)$  denotes the set of successors of $A$ in $T_\varphi$ .

Example for $A_3$ in the [Tableaux](Tableaux.md) below $\sigma(A_3)=\{A_3,A_2,A_0,A_4,A_6\}$

![](Verification%2033_image_1.png)

### 1.6.3 The [[behavior graph]]
Given a finite-state program $P$ and an [LTL](temporal%20logic.md) formula $\varphi$, we construct the [behavior graph](behavior%20graph.md) of $(P,\varphi)$ denoted as $B_{(P,\varphi)}$ as the product of the graph for $P(G_p)$ and the [Tableaux](Tableaux.md) for $\varphi(T_\varphi)$.

What are the part of the [behavior graph](behavior%20graph.md)?
1. **nodes** $(s,A)$ where $s$ is a state of the program $P$ and $A$ is an [Atom](Atom.md) consistent with $s$.
2. **Edges:** There exists a $\tau$-labeled edge from $(s,A)$ to $(s',A')$ only if $s'$ is a $\tau$-successor of $s$ i.e. $s'\in \tau(s)$ and $A'$ is in the set of successors of $A$ i.e. $A'\in \delta(A)$ in the pruned table $T_\varphi$  .
3. **initial $\varphi$-node** are pairs $(s,A)$ where $s$ is an initial state for $P$, $A$ is an initial $\varphi$-atom in $T_\varphi$ (that is,$\varphi \in A$) and $A$ is consistent with $s$.
	This means that the initial states are the initial states for the program ($s$) and the initial state for the [Tableaux](Tableaux.md) ($\varphi$-atom)

#### 1.6.3.1 The algorithm to build the [behavior graph](behavior%20graph.md)

Algorithm **BEHAVIOR-GRAPH:**
- Place in $B_{(P,\varphi)}$ all initial $\varphi$-nodes $(s, A)$
- Repeat until no new nodes or new edges can be added the following steps.
	Let $(s, A)$ be a node in $B_{(P,\varphi)}$ , let $\tau \in T$ be a transition, and let $(s',A')$ be a pair such that: 
	-  $s'$ is a $\tau$ -successor of $s$, where $A' \in \delta(A)$ in the pruned tableau $T_\varphi$ 
	-  $A'$ is consistent with $s'$
	
- Add $(s',A')$ to $B_{(P,\varphi)}$ , if it is not already there.
- Draw a $\tau$ -edge from $(s, A)$ to $(s', A')$ if it not already there. (sometimes it can be the case that the node is already there but not an edge)

### 1.6.4 Example for behavior graphs:
The system loop
initialy $x=1$
Transitions:
1. the $Idling$ transition $\tau_I$ 
2. $\tau$ with transition relation $\rho_{\tau_2}=(x+1) \enspace mod(4)$

The set of [Just](Justice.md) transitions is $J={\tau}$

Let us consider the [LTL](temporal%20logic.md) formula: $\psi_3:$ $F(G(x \not = 3))$
The formula means that from one point in the future $x$ will always be unequal from $3$.

One possible computation that would make the computation valid is $\tau_I^\omega$ but there is one problem as we demand [Justice](Justice.md) for $\tau$ it has to be taken at some point, making all computations impossible where $\tau_I$ is used infinitely many times. The [Justice](Justice.md) requirement demands us to not always stay in one state but move from time to time to the next one.

This means: ==It is impossible to prevent us to go through $s_3$ infinitely many times==
The formula is [insatisfiable](Satisfiability.md)!

If we interpret the formula as the negation i.e. $\neg \psi_3 = G(F(x=3))$ is [Valid](Validity.md)


![](Verification%2033_image_4.png)



#### 1.6.4.1 The [Tableaux](Tableaux.md) to the program
![](Verification%2033_image_5.png)


>[!Note] We have two logical variables
>1. $x=3$
>2. $x\neq 3$

The notation is a little bit different from the one we are used to, it is called **state-chart representation**. 
1. We have two graphs. This comes from pruning i.e. the removal of nodes. The graph without pruning is one graph.
2. The individual atoms are written like that, that if they share all components except one, they are written as one node, writing down the difference next to the Atom name. For instance $A_0$ and $A_1$ are only different by one formula. The formulas written out for $A_0$ and $A_1$ are the following, they only differentiate themselfs by $A_0$ having $x=3$ inside and $A_1$ having instead $x \not = 3$ inside i.e.
	- $A_0=\{(x=3),\underbrace{\neg \psi_3,\neg F(x\neq 3),\neg G(\psi_3),\neg G(F(x\neq3)}_{same}\}$
	- $A_1=\{(x\neq 3),\underbrace{\neg \psi_3,\neg F(x\neq 3),\neg G(\psi_3),\neg G(F(x\neq3)}_{same}\}$
3. If there is a edge from a macro Atom to another Atom, all micro Atoms have edges to the other Atom.

Now we can prune even more:
We can remove all not $\psi$-reachable nodes which are: $A_0,A_1,A_2$ leaving us with the lower part of the [behavior graph](behavior%20graph.md).

![](Verification%2033_image_6.png)

### 1.6.5 The entire [[behavior graph]]

Now we merge the [Tableaux](Tableaux.md) and the program graph to one big behavior graph:

![](Verification%2033_image_7.png)

The edges are labeled with the transitions from the program-graph.

How do we create this we look at the states and which logical variables are true:

- $s_0: x=0 \rightarrow x \not = 3$
- $s_1: x=1 \rightarrow x \not =3$
- $s_2: x=2 \rightarrow x\not=3$
- $s_3: x=3 \rightarrow x=3$
Atoms with $x \not = 3$
- $A_3$,$A_5$,$A_7$
Atoms with $x=3$
- $A_4,A_6$

As the initial state of the program is: $s_0$ and the only two nodes that are [consistent](VV%20consistent.md) are: $A_3,A_5,A_7$:
$A_3$ does not have a exit meaning it eliminates itself. So we have two starting nodes: $A_5,A_7$

When we use $\tau$ in $A_5$ we stay in the same atom but the state changes first from $s_0$ to $s_1$ then to $S_2$. When we apply $\tau$ one more time $x=3$  meaning that $A_5$ is not anymore consistent with the state. This means that we need to change atom.
![](Verification%2033_image_8.png)

We can go to one of the two atoms that have $x=3$ i.e. $A_4$ or $A_6$ which is represented in the [behavior graph](behavior%20graph.md) by the two edges from the state $(s_2,A_5)$ to either $(s_3,A_4)$ or $(s_3,A_6)$ as shown in the image below.

![](Verification%2033_image_9.png)

Now we are restricted by the [Tableaux](Tableaux.md). When we are in $A_4$ we have three choices, either we stay in $A_4$ we go to $A_5$ or we go to $A_6$. $A_6$ only has one exiting edge meaning we need to go to $A_7$. The two options are shown below in the image.

![](Verification%2033_image_10.jpeg)
The equivalent connections in the [behavior graph](behavior%20graph.md) are the following:
![](Verification%2033_image_11.png)

When we start in state 7 there is only two options the idle operation $\tau_I$ and the increment i.e. $\tau$. We can use this two times, then we can only do $\tau_I$ because then the Atom $A_7$ does not have an outgoing edge...


#### 1.6.5.1 What is a path in $B_{(P,\psi)}$?
It is a infinite sequence of tuples i.e. path $\pi=(s_0,A_0),(s_1,A_1),(s_2,A_2),(s_3,A_3)\dots$
It is necessary for $(s_0,A_0)$ to be a $\psi$-node i.e. the Atom $A_0$ needs to contain $\psi$. It is a valid path if and only if both components, one from the program  ($\sigma_\pi$) one from the [Tableaux](Tableaux.md) ($\theta_\pi$)have certain properties:
- $\sigma_\pi:s_0,s_1$ is a [run](run.md) of P
- $\theta_\pi:A_0,A_1$ is a [trail](trail.md) of $T_\varphi$ over $\sigma_\pi$ (for all $j \ge 0, A_j$ is consistent with $s_j$)

Lets do some examples:
in the program $B_{(LOOP,\psi_3)}$ we choose the following path:
- $\pi:((s_0,A_5),(s_1,A_5),(s_2,A_5),(s_3,A_4))^\omega$
This induces the following two components:
- $\sigma_\pi:(s0,s1,s_2,s_3)^\omega$
- $\theta_\pi:(A_5,A_5,A_5,A_4)^\omega$

#### 1.6.5.2 How do we check p-[satisfiability](Satisfiability.md) now?

Both components ($\sigma,\theta$) of a path ($\pi$) through a program $B_{(P,\varphi)}$ need to have certain requirements:
- $\sigma_\pi$ needs to be a [Fair](Fair.md) run
- $\theta_\pi$ is a [fullfilling trail](fullfilling%20path.md) over $\sigma_\pi$


==Example:==
When we choose the following path also introduced above:
- $\pi:((s_0,A_5),(s_1,A_5),(s_2,A_5),(s_3,A_4))^\omega$
- $\theta_\pi:(A_5,A_5,A_5,A_4)^\omega$ is not a [fullfilling path](fullfilling%20path.md).
	Why? it contains $\psi$ which is the promise: $F(G(x\neq3)$ but it does not [fullfill](fullfilling%20path.md) the promise. To fullfill the promise it should contain either the enclosed formula $G(x \neq 3)$ or the negation of the promise itself i.e. $\neg F(G(x\neq3)$  [Promise](Promise.md)

Or we choose another path:
$\pi=(s_0,A_7),(s_1,A_7),(s_2,A_7)^\omega$

In terms if this is a [fullfilling path](fullfilling%20path.md) the path is not fullfilling as it contains the promise $F(G(x\neq3))$ but does not contain $G(x\neq3)$ or $\neg F(G(x\neq3))$

But here we have also a breach of justice, because when we end up in $(s_2,A_7)$ we always need to take the idle transition $\tau_I$, and as $\tau$ is enabled but never taken it breaks the [Justice](Justice.md) condition.

Hereby we can conclude that there is no computation that satisfies $\psi$.

#### 1.6.5.3 Now lets give a full algorithm to satisfiability checking: [[Adequate subgraphs]]

Given a [behavior graph](behavior%20graph.md) $B_{(P,\varphi)}$ and a sub-graph $S \subseteq B_{(P,\varphi)}$.

- node $(s' , A')$ is a **$\tau$ -successor** of node $(s, A)$ if $B_{(P,\varphi)}$ contains a $\tau$ -edge connecting $(s, A)$ to $S',A')$ 
- transition $\tau$ is **enabled** on node $(s, A)$ if it is enabled on state $s$
- transition $\tau$ is taken in $S$ if there exist two nodes $(s, A)$ and $(s',A')$ in $S$ such that $(s',A')$ is a $\tau$-successor of $(s, A)$
- $S$ is [Just](Justice.md) if every just  transition $\tau \in J$ is either taken in $S$ or is ==disabled on some nodes==  in $S$
- $S$ is [Compassionate](Compassion.md) if every compassionate transition $\tau \in C$ is either taken in $S$ or is ==disabled on all nodes==  in $S$
- $S$ is [Fair](Fair.md) if it is both [Compassionate](Compassion.md) and [Just](Justice.md)
- $S$ is an [Adequate subgraph](Adequate%20subgraphs.md) if it is [Fair](Fair.md) and [fullfilling](fullfilling%20path.md)
The summarizing Proposition:
>[!Proposition]
>A finite-state program $P$ has a computation $\sigma$ which satisfies $\varphi$ if and only if the [behavior graph](behavior%20graph.md) $B_{(P,\varphi)}$ has an adequate strongly connected subgraph

Example, as already shown above the program $LOOP$ and the [LTL](temporal%20logic.md) formula $\psi_3=F(G(x\neq 3))$ does not have an [Adequate subgraph](Adequate%20subgraphs.md) and is hereby not [satisfiable](Satisfiability.md).

![](Verification%2033_image_7.png)

Why:
First subgraph is not fullfilling
$((s_0,A_5),(s_1,A_5),(s_2,A_5),(s_3,A_4))^\omega$
Second subgraph only containing
$(s_3,A_6)$ is [transient](transient%20node.md) therefore we do not consider it.
The last one is not [Fair](Fair.md) (as it is not [Just](Justice.md))
$(s_0,A_7),(s_1,A_7),(s_2,A_7)^\omega$

From the class:
![](Verification%2033_image_12.png)


Another example: Lets check for [satisfiability](Satisfiability.md) of the negation of our formula $\neg \psi_3=\phi_3=G(F(x+3))$

![](Verification%2033_image_13.png)


$A_0$ is fullfilling as it has the promise $F(x=3)$ and the formula fullfilling the promise $x=3$.

$A_1$ is not fullfilling as it it has the promise $F(x=3)$ and but no formula to fullfill the promise.

![](Verification%2033_image_14.png)

We can imagine a path $((A_1,s_0),(A_1,s_1),(A_1,s_2),(A_0,s_3))^\omega$ as it is a [fullfilling path](fullfilling%20path.md) as it contains an atom that is fullfilling its promisses.
Further it is [Just](Justice.md) as we use all transitions that are enabled the same is true for  [Compassion](Compassion.md)

---
34 b

---

#### 1.6.5.4 Why can [Compassion](Compassion.md) be a problem?
Checking the [MSCS](VV%20Strongly%20connected%20subgraph.md) is not enough for [Fairness](Fair.md) of the [Path](Path.md).

Why?
If the [MSCS](VV%20Strongly%20connected%20subgraph.md) $S$ has [Justice](Justice.md) also all subgraphs $S'$ have [Justice](Justice.md).

BUT:
If a subgraphs $S'$ has [Compassion](Compassion.md) it does not imply that the [MSCS](VV%20Strongly%20connected%20subgraph.md) has [Compassion](Compassion.md)

Lets do an example:
$S'$ compassionate **do not imply** $S$ compassionate

Let $\tau_2$ belong to the set of compassionate transitions. $\tau_2$ is enabled on $s2$ and disabled on $s1$.

The path $((s_1,A_3),(s_2,A_4))^\omega$ does not have [Compassion](Compassion.md). We pass infinitely many times through $(s_2,A_4)$ but even though it is switched on and off, it is never taken.

Now lets look at the subgraph $S'$ $(s_1,A_3)^\omega$ this one has [Compassion](Compassion.md).



![](Verification%2033_image_15.png)

## 1.7 Lets build a algorithm $ADEQUATE-SUB$
Algorithm $ADEQUATE-SUB$
- accepts as input a strongly connected subgraph $S$ and returns as output a strongly connected subgraph $S' \subseteq S$
- (If $S' = \emptyset) - that means that $S$ contains no adequate subgraphs
- (else) - This means that $S'$ is an adequate strongly connected subgraph in $S$

Notation:
- $EN(τ, S)$ - the set of all nodes $(s, A)$ in $S$ on which $\tau$ is enabled

The algorithm:
![](Verification%2033_image_16.png)

Lets apply the algorithms on a program: $LOOP+$:

![](Verification%2033_image_17.png)

Initially $x=0$
[LTL](temporal%20logic.md) formula: $F(G(x\neq3))$
Transitions:
1. the idling transition $\tau_I$
2. $J=\{\tau_1,\tau_2\}$
3. $C=\{\tau_3\}$
New [MSCS](VV%20Strongly%20connected%20subgraph.md): $S=\{(s_0,A_7),(s_1,A_7),(s_2,A_7)\}$

The Pruned [Tableaux](Tableaux.md):
![](Verification%2033_image_18.png)

The [behavior graph](behavior%20graph.md) $B(LOOP+,\psi_3)$
![](Verification%2033_image_19.png)

Some of the transitions are not anymore allowed due to [Compassion](Compassion.md).
For instance: $((s_0,A_5),(s_1,A_5),(s_2,A_5),(s_3,A_4))^\omega$
As $\tau_3$ is always enabled but never taken

Is $\psi_3$ satisfiable? No because of the compassion for $\tau_3$. We need to avoid $s_3$ but we need to take $\tau_3$ at least once.

Lets look at the [VV MSCS](VV%20Strongly%20connected%20subgraph.md) $S={(s_0,A_7),(s_1,A_7),(s_2,A_7)}$

- [fullfilling?](fullfilling%20path.md) Yes, because $A_7$ is fullfilling
- [Just](Justice.md)? $\tau_1$ and $\tau_2$ are taken infinitely many times.
- [Compassionate](Compassion.md)? Thats the problem $\tau_3$ is never taken but enabled in $(s_1,A_7)$

What is a fix for this? We remove $(s_1,A_7)$? And get a smaller subgraph

![](Verification%2033_image_20.jpeg)


- [fullfilling?](fullfilling%20path.md) Yes, because $A_7$ is fullfilling
- [Just](Justice.md)? $\tau_1$ and $\tau_2$ are taken infinitely many times.
- [Compassionate](Compassion.md)? Indeed as we solved the problem with compassion by eliminating the only node that had a computation that had [Compassion](Compassion.md).

Hence the system $LOOP+$ has a computation $\sigma:(s_0,s_1)^\omega$ that [Satisfies](Satisfiability.md) $\psi_3=F(G(x\neq3))$

We have the algorithm [SAT](SAT.md) to check whether a [LTL](temporal%20logic.md) formula $\varphi$ is satisfiable.

We have the algorithm [[P-SAT]] to check the [Satisfiability](Satisfiability.md) of a formula $\varphi$ over a program (to check whether a finite-state program $P$ has a
computation which satisfies a temporal formula $\varphi$)

What are the [P-SAT](P-SAT.md) steps for the program $P$ and the formula $\varphi$:
1. Construct the state-transition graph $G_p$
2. Construct the pruned [Tableaux](Tableaux.md) $T_\varphi$
3. Construct the [behavior graph](behavior%20graph.md) $B_{(P,\varphi)}$
4. Decompose $B_{(P,\varphi)}$ into [MSCS](VV%20Strongly%20connected%20subgraph.md) $S_1,\dots,S_t$
5. For each of the [MSCS](VV%20Strongly%20connected%20subgraph.md) apply the algorithm $ADEQUATE-SUB$ to identify [Adequate subgraphs](Adequate%20subgraphs.md)

If any of these applications returns a nonempty result, $P$ <mark style="background: #014E11F2;">has a computation satisfying</mark> $\varphi$.

This computation can be constructed by forming a path $\pi$ that leads from an initial node to the returned adequate subgraph $S$, and then continues to visit each node $S$ infinitely many times. The desired computation is the computation $\delta_\pi$ induced by $\pi$. If all applications return the empty set as result, $P$ has no computation satisfying $\varphi$.

To check P-validity of a formula $\varphi$, apply algorithm [P-SAT](P-SAT.md) to check whether there are P-computation satisfying $\neg \varphi$

- If there is a P-computation satisfying $\neg \varphi$, then $\varphi$ is not P-valid

- If there are no P-computations satisfying $\varphi$, then $\varphi$ is P-valid [Validity](Validity.md)

