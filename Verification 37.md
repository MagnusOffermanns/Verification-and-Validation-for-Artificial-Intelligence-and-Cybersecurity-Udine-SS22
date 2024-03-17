# 1 [Model-checking](Model-checking.md): how to cope with the State explosion Problem

The main disadvantage of [Model-checking](Model-checking.md) is [[State explosion]] that can occur if the system being verified has many components that make transitions in parralel.

The parallel composition of two concurrent components is indeed modele by taking the [Cartesian Product](Cartesian%20Product) of the corresponding [state space](state%20space)s: The global [state space](state%20space) of a reactive system may grow ==exponentially== with the number of concurrent processes running in the system.

The expolorion of such a huge state space may be prohibitive even for an algorithm running in linear time in the size of the model.


## 1.1 Possible solutions to the state explosion probem
There are two  main approaches:
- [[Symbolic model-checking]]
- [[Partial Order reduction]]

The role of [Binary Decision Diagrams](Binary%20Decision%20Diagram.md) (for synchronous circuits):
Data structures for the representation of Boolean functions, that make it possible to obtain concise representations for transition systems and to manipulate them quickly.

To deal with asynchronous protocols, the size of the search space can be reduced by using the [Partial Order reduction](Partial%20Order%20reduction.md).

# 2 [Symbolic model-checking](Symbolic%20model-checking.md)

Was proposed by McMillan in 1991. It replaes fixed-point computations over individual states by manipulations of definitions of state sets. It allows an exhaustive implicit enumeration of a huge number of states.

==We do not enumerate over individual states like in traditional model-checking but over set of states.==

- states: bit vectors of fixed length $m$
- $S\subseteq \{0,1\}^m:$ defined by a [[Boolean formula]] $\beta_S(x_1,\dots,x_m)$
	Defines the states. If we have four states this should look like this
	$(1,0,0,0),(0,1,0,0),(0,0,1,0),(0,0,0,1)$
- $R\subseteq S \times S:$ defined by a [[Boolean formula]] $\beta_R(x_1,\dots,x_m,x_1',\dots,x_m')$
	Defines the edges between the states
	If the first state has connections to state 2 and 3 one would write: 
	$((1,0,0,0),(0,1,1,0))$
- $L: S \rightarrow 2^\{P_1,\dots,P_n\}:$ defined by a [[Boolean formula]] $\beta_1(x_1,\dots,x_m),\dots,\beta_n(x_1,\dots,x_m)$ (where $\beta_i$ defines the set $\{s \in S: P_i \in L(S)\}$)
	Defines which propositional letters are true in which state.
	If we want to say that in propostional letter three i.e. $P_3$ is true in state 2 and three we would write:
	$\beta_3(0,1,1,0)$

This structure is similar to the temporal structure we introduced in [CTL](Branching%20time%20temporal%20logic.md).


Now the question is: How do we represent temporal structures in Boolean formulas?

==Example:==

$x_i= x(t)$
$x_i'=x(t+1)$

Let $S=\{0,1\}^3$ and the the "target" state be defined by $S=(1,1,0)$ i.e. $x_1 \land x_2 \land \neg x_3$ .

Let $R$ be defined by:
$$R=\bigwedge_{i=3}^{3}(x_i \implies x_i')\land (x_1 \iff x_1' \lor x_2 \iff x_2')$$
What does this mean?
- $(x_i \implies x_i')$
	If $x_i$ is true it must be true in the next state as well. i.e. If $x_i$ ever becomes true it has to stay true.
- $(x_1 \iff x_1' \lor x_2 \iff x_2')$
	At least one of the values $x_1$ or $x_2$ need to be preserved in a transition. I.e. In a transition we can only change either $x_1$ or $x_2$

We want to solve the boolean formula $E(F(target)) \equiv E(F(x_1 \land x_2 \land \neg x_3))$

Now we do not go from a initial state to a final state, but we do it the other way around, we start in the final state and go back, finding a path to the initial state

We start at the $target$ state: $x_1 \land x_2 \land \neg x_3$ 

Then we go one state back by the following operation:
$target \cup E(X(target))$

We apply the two allowed transfers (after ($R$) )and or them to the initial state which are:
1. $(\neg x_1 \land x_2 \land \neg x_3)$
2. $(x_1 \land \neg x_2 \land \neg x_3)$
$$(x_1 \land x_2 \land \neg x_3) \lor (\neg x_1 \land x_2 \land \neg x_3) \lor (x_1 \land \neg x_2 \land \neg x_3)$$

Then we go another step back i.e. add $E(X(E(X(target))$
$$(x_1 \land x_2 \land \neg x_3) \lor (\neg x_1 \land x_2 \land \neg x_3) \lor (x_1 \land \neg x_2 \land \neg x_3) \lor (\neg x_1,\neg x_2,\neg x_3)$$

 Now whenever we add another $EX$ we can not add other binary formulas. The set of binary formulas stays the same.

When we simplify this, we see that we have all permutations of $x_1$ and $x_2$ so we can just ommit this two variables and say all starting states are good in which $x_3$ is false (as we are not allowed to change it)  i.e. 
$$target \cup EX(target) \cup EX(EX(Target)=EF(Target)=\neg x_3$$
The full structure looks like this:  

![](Verification%2037_image_1.png)

---

37 b

---

Summarzing what are the two key steps:
- proceed from a set of states $T$ to the predecessor of $T$ i.e. $\{s \in S | \exists(s,s') \in R: s' \in T\}$
	If there is a node from $s$
	to $s'$ where $s'$ is the predecessor we add it to $T$
 - proceed from a formula $\beta_T(\bar{x})$ to $\beta_T(\bar{x})'=\exists\bar{y}(\beta_R(\bar{x},\bar{y})\land \beta_T(\bar{y}))$ 
	 This says the same as the formula before just written differently 


>[!Problem]
>What is a good normal form for the representation of [Boolean formula](Boolean%20formula.md) which allows efficient application of $\neg, \land, \lor \text{ and } \exists$

## 2.1 [[Ordered Binary Decision Diagramm]]

They are a reduced version of [Decision Tree](Decision%20Tree.md)s for boolean function

![](Verification%2037_image_2.png)



Starting from a normall [Binary Decision Diagram](Binary%20Decision%20Diagram.md)

- Merge any [isomorphic](https://en.wikipedia.org/wiki/Graph_isomorphism "Graph isomorphism") subgraphs.
- Eliminate any node whose two children are isomorphic.

$\neg,\lor,\land,\exists$ can be performed on [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)s.

## 2.2 Partial order reduction
[Partial Order reduction](Partial%20Order%20reduction.md) can be used to reduce the size of the state space by making use of the following observations:
>[!Note]
>Computations that differ in the ordering of Indepenently executed Events are usually indistinguishable byt he specification  and thus they can be considered equivalent

For instance:
If we have the computations $a,b,c,d,e$ and only $a$ and $d$ are influencing each other i.e. are not independent. Then it does not differ if I run the computation:
- $a,c,e,d$
or
-  $a,b,e,d$

The results of the computations are equivalent

Now we need to identify classes which computations are equivalent. Then we only need to check only one representative of each class.

It suffices to check a reduced sate space, which contains (at least) one representative computation for each class of equivalent computations.


## 2.3 Further Advanced techniques
- Bounded [Model-checking](Model-checking.md)
	Sat solvers + symbolic model checking + bounded models 
- Satisfiability Modulo Theories (SMT sovers)
	satisfiability formulas with respect to one or more backgroun theories formulated in first-order logic with equality (integers, real numbers etc...)
- K-Liveness
	a simple but effective technique for [LTL](temporal%20logic.md) verification, it checks the absence of lasso-shaped conterexamples by trying to prove that bad sattes are visited at most k times for increasing values of k (liveness checking as a sequence of safety checks)
- iC3:
	A very successful SAT-based model checking algorithm based on induction



## 2.4 A detailed account of [Symbolic model-checking](Symbolic%20model-checking.md). 

### 2.4.1 [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)
They can be used to represent  [Finite State transition systems](Finite%20State%20Automata.md) in a compact and effective way.

1. We have to find a represent [Boolean functions](Boolean%20formula.md)
2. How to efficiently implement logical operations and existential quantification ($\land,\lor,\neg,\exists$) 

The starting point are [Binary Decision Trees](Binary%20Decision%20Diagram.md).

#### 2.4.1.1 Notation and terminology:
We have two types of nodes:
1. non terminal nodes (internal nodes)
2. terminal nodes (leaf nodes)

Eah on terminal node $v$ is labeled by a variable $var(v)$ in the example above this were $x_1,x_2,x_3$. Which is the variable associated to the node and has two successors. $Low(v)$ is the left successor and $high(v)$ which is the right successor.

Each terminal node $v$ is labeled by a value (either $0$ or $1$).

Example: two bit comparator

$f(a_1,a_2,b_1,b_2): (a_1 \iff b_1) \land (a_2 \iff b_2)$ 

The two-bit comparator can be represented by the following decision tree:

![](Verification%2037_image_3.png)

There is a lot of redundancy.

Another problem is that the tree looks different if we order the variables differently for instance $(b_1,a_2,a_1,b_2)$ etc.

To reduce redundancy we replace the [Binary Decision trees](Binary%20Decision%20Diagram.md) to [Binary Decision Diagram](Binary%20Decision%20Diagram.md)s.

They are: directed acyclic and a graph
We wil use [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) which stands for
[[BDD]] + a total ordering of the variables [[Binary decision tree]].

In an [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) each non-terminal node is labeled by a variable $v$ and has two successors $low(v)$ and $high(v)$. Terminal nodes are labeled by $0$ an $1$.

 Formerly, every [Binary Decision Diagram](Binary%20Decision%20Diagram.md) with  root $v$ defines a Boolean function $f_v(x_1,\dots,x_n)$ as follows:
 1. if $v$ is a terminal node:
	 - if value of $v$ is $1$, then $f_r(x_1,\dots,x_n)=1$
	 - if value of $v$ is $0$, then $f_r(x_1,\dots,x_n)=0$
2. if $v$ s a non-terminal node with $var(v)=x_i$, then $f_r$ is the function:
	$f_r(x_1,x_2,\dots,x_n)=(\neg x_i \land f_{low(v)}(x_1,x_2,...x_n)) \lor x_i \land f_{high(v)}(x_1,x_2,...x_n))$ 

The ultimate goal is to find compact and effective canonical representation of the Boolean function.

The [Equivalence](Equivalence.md) of two function becomes [isomorphism](isomorphic.md) of their [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) representation.

>[!note]
>This checks for equivalence make sense only if the orderings of the variables meaning the two [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) are the same.

How do we remove isomorphic subtrees as seen in the example above. Further we need to remove redundant nodes.

 We repeatedly apply the following transformation rules:
 - remove duplicated terminals:
	 Eliminate all but one of the terminal nodes with a given label and redirect all the incoming edges of the eliminated nodes to the remaining node.
- remove duplicate non terminal nodes:
	If two non-terminal nodes $u$ and $v$ are such that $var(u)=var(v) \land low(u)=low(v) \land high(u)=high(v)$ then eliminate $u$ or $v$ and redirect all incoming edges to the remaining node.
- remove redundant tests:
	if a terminal node $v$ is such that $low(v)=high(v)$  then eliminate the node $v$ and redirect all incoming edges to $low(v)$. 


An example of appication of the removal of redundant tests is the following:

Example:

![](Verification%2037_image_4.png)


The branches after $a_2$  which lead to the node$b_2$ are the same we can summarize them as they both arrive at $0$. We remove redundant test leading us to the following tree:

![](Verification%2037_image_5.png)


Now we can apply again the same rule, as whenever we go towards $a_1$ we reach 0, we remove $a_1$.

![](Verification%2037_image_6.png)



Example:
For the big tree we painted above the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) would look like this:

![](Verification%2037_image_7.png)

Now we apply the ==rule of duplicate non terminals== two times:
Once the nodes 1+2 and the nodes marked as 3+4.

![](Verification%2037_image_8.png)

The resulting graph looks like this

![](Verification%2037_image_9.png)

By another application of ==duplicate non terminals== we remove the following nodes:


![](Verification%2037_image_10.png)

The final diagram looks like this:

![](Verification%2037_image_11.png)

This result has only 8 nodes, in comparison to the 31 nodes of the original tree.

If you take the alternative variable ordering $a_1,a_2,b_1,b_2$ one gets a different [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) with 11 nodes. There is a small increase of nodes compared to the other ordering i.e. $a_1,b_1,a_2,b_2$.

What does this tell us for the n-bit comparator?

1. ordering $a_1,a_2,b_1,b_2$
	resulting nodes: $3 \cdot 2^{n-1}$
	This is exponential growth
2. ordering $a_1,b_1,a_2,b_2$.
	resulting number of nodes: $3n+2$
	This is much better

Unfortunately finding a optimal ordering but also checking whether a given ordering is optimal is [NP-complete](NP%20problems.md) problem. Meaning that there is no clever way to find a optimal ordering. One has to explore all solutions.

Nonetheless a couple of [Heuristics](Heuristics.md) have been explored. 

### 2.4.2 The $Restrict$ function

Let us introduce a auxiliary function $RESTRICT$ that allows to restrict some variable for instance $x_i$ of a boolean function $f$ to take a constant value $b$ ($b$ can either be $1$ or $0$)) we denote such a function by:
$$f|_{x_i \leftarrow b}$$
It satisfies the following identity: $f|_{x_i \leftarrow b}(x_1,x_2,\dots,x_n) = f(x_1,\cdots,x_{i-1},x_i=b,x_{i+1})$

==Example:==
Take the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) in canonical form for the two bit comparator and restrict it to $b_1 \leftarrow 0$:
In this case the node $b_1$ disappears from the diagram.

![](Verification%2037_image_12.png)

The resulting [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) is the following:

![](Verification%2037_image_13.png)

Exercise for home: Restrict the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $b_1 \leftarrow 1$


![](Verification%2037_image_11.png)

>[!Note] Remark
>Such a transformation does not guarantee in general that the resulting [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) is in canonical form. Then one needs to check whether it can be further simplified. 
>Canonical -> most simplyfied state.

>[!Note] The general rule of $Restrict$ 
>For any node $v$ which has an entering edge to a node $w$ such that $var(w)=x_i$, where $x_i$ is the variable we want to restrict, we replace the node $w$ by $low(w)$ if $b=0$ and $high(w)$ if $b=1$.
>![](Verification%2037_image_14.png)

==Up to now:==
- [Boolean formula](Boolean%20formula.md)/functions
- [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) (in canonical form)
- Auxiliary function $Restrict$


### 2.4.3 How can we implement the two argument logical operations efficiently on [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)s?
$2^4=16$ operations.

We use [[Shannon-Expansion]]s
$f(x)=(\neg x \land f|_{x \leftarrow 0}) \lor (x \land f|_{x \leftarrow 1})$

We split $f(x)$ up into two part.
1. Either $x=0$ then we can force $x$ to $0$ i.e. $f|_{x \leftarrow 0}$
2. Or we force $x=1$ then we can force $x$ to $1$ i.e. $f|_{x \leftarrow 1}$

The result are two simpler function that can easier be handled. It looks trivial but is nice for bigger formulas.

Lets say we have a lot o occurences of $x \land y$ and we force $x$ to be 0, we get twice the amout of formulas but every occurence of $x \land y$ can be evaluated as $0$ removing complexity.

---

End 38 b

--- 

We define the algorithm called $APPLY$ to efficiently compute all the 16 logical operations:

Let $*$ be one of these logical operations and let $f$ and $f'$ be two [Boolean function](Boolean%20formula.md)s that we want to combine by the operation start i.e. $f() * f'()$.

==Assumptions:==
Let $v$ and $v'$ be the roots of the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) of the functions $f$ and $f'$ respectively and $x=var(v)$ and $x'=var(v')$. (If $v$ and $v'$ are terminal nodes they are labeled by $0$ or $1$).

The two functions operate on the same set of variables in a unique ordering of the variables, similar for both [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)s.

WE consider some cases depending on the relationships between $v$ ad $v'$ (the roots of the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)).

Now we consider multiple cases:

1. Basecase:
	I $v$ and $v'$ are terminal nodes then the compositions is: $f() * f'()=value(v) * value(v')$
2. if $x=x'$ where $x$ is the variable associated with $var(v)$ and $x'$ is the $var(v')$:
	We apply [Shannon-Expansion](Shannon-Expansion.md) as follows: $$f *f'=(\neg x \land (f|_{x\leftarrow0} * f'|_{x\leftarrow0})) \lor  (x \land (f|_{x\leftarrow 1} *f|_{x\leftarrow 1})$$
3. if $x < x'$ i.e. the roots of the trees are different, and x appears somewhere above $x'$ in the tree i.e. the ordering is like that so that $x$ is before $x'$ ($RESTRICT$ does not have an effect on $f'$ i.e.  $f|_{x \leftarrow 0}=f|_{x \leftarrow 1} = f'$
	Then we apply [Shannon-Expansion](Shannon-Expansion.md) like this:
	$f*f'=(\neg x \land (f|_{x\leftarrow 0} * f') \lor  (x \land (f|_{x\leftarrow 1} *f')$
4. if $x' < x$ it is very similar to point 3.
	$f*f'=(\neg x \land (f * f'|_{x\leftarrow 0)} \lor  (x \land (f *f'|_{x\leftarrow 1})$

If we proceed in a blind way we can repeat the same expansion for all cases. Every time we double the number of formula pairs we have to consider, there is ==no advantage== as the number of pairs increases exponentially.

>[!Note] Remark
>Each subproblem can in principle generate two other subproblems, and thus the algorithm if blindly applied may involve a exponential blowup.
>Luckily it is possible to prevent the algorithm from beeing exponential. We see now how this prevention works.

Each sub-problem corresponds to a pair of [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) that are subgraphs of the original [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)s. Since each subgraph is univocally identified by its root, the number of distinct subgraphs in the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $f$ (and the same is true for $f'$) is defined by the size of the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md).

This means that the same subparts of the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) are used therefore the number of formulas is bounded by the size of the  original [OBDD](Ordered%20Binary%20Decision%20Diagramm.md).

So the number of distinct subproblems (maynly pairs) is bounded by the product of the size of the orginal [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $f$ and $f'$.

We can use a [[Hash table]] to keep track of previousely solved sub-problems and must be accessed before explicitly solving a new subproblem to check whether it was already solved before.

#### 2.4.3.1 The special case of negation

A special case is that of negation, but one might say it is a [unary operator](unary%20operator.md), how can we interpret it as a binary operator?

We can present it as follows:
$$\neg x_1 = (\neg x_1 \land \neg x_2) \lor (\neg x_1 \land x_2)$$

However the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for the negation of a function $f$ can be contained from the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) from $f$ by swapping the terminal nodes.

>[!Note]  [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) of a negated function
>the negation of a function $f$ can be contained from the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) from $f$ by negating the values of the terminal nodes (leafs) i.e. $1$ becomes $0$ and $0$ becomes $1$.

### 2.4.4 Representing [Kripke structure](Kripke%20structure.md)s by means of [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)s
The [Kripke structure](Kripke%20structure.md) is a struture of the form:
$$M=\{S,R,L\}$$
We want to start with some observations already stated in the introductory part.

1. Each relation of $n$ arguments i.e. $Q(x_1,x_2, \dots x_n)$ can be represented by their characteristic function
	$Q(x_1,x_2, \dots x_n)=$
	$f_q(x_1,x_2, \dots x_n)=1$
	$f_Q$ only takes the value $1$ on all and only those tuples belonging to $Q$

	$M=(S,R,L)$ be a [Kripke structure](Kripke%20structure.md).
2. $S$: let the kardinality of $S$ for some $m$ be $|S|=2^m$
	The [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $S$ is the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for the following formula
	$$(\neg x_1 \land \neg x_2 \land \dots \neg x_m )\lor (\neg x_1 \land \neg x_2 \land \dots x_m ) \lor \dots \lor (x_1 \land x_2 \land \dots  x_m ) \equiv 1 $$
	Each of the brackets represent one state. i.e. $(\neg x_1 \land \neg x_2 \land \dots \neg x_m )$ represents state 1, $(\neg x_1 \land \neg x_2 \land \dots x_m )$ represents state 2 etc.
	As as tehe function always returns 1 we can represent $S$ as the following tree:
	![](Verification%2037_image_15.png)
	I.e. the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) can be represented as a 1 leaf with the value $1$
	![](Verification%2037_image_16.png)
3. $R$  is a relation over variables $x_1,x_2,\dots x_m,x_1',x_2',\dots,x_m'$ 
==Example:== 

![](Verification%2037_image_17.png)
How do we represent $R$?
1. edge $11$ to $10$
	$x_1\land x_2 \land x_1' \land \neg x_2'$
2. edge $10$ to $11$
	$x_1\land \neg x_2 \land x_1' \land  x_2'$
3. edge $10$ to $10$
	$x_1\land \neg x_2 \land x_1' \land \neg x_2'$
The entire function looks then like this:
$$(x_1\land x_2 \land x_1' \land \neg x_2') \lor (x_1\land \neg x_2 \land x_1' \land  x_2') \lor (x_1\land \neg x_2 \land x_1' \land \neg x_2')$$

3. $L$ the Labeling function:
	Instead of specifying for each state which proposition letters are true in it, we define for each proposition letter, the set of states where they are true. That is for each proposition letter $p$ we specify $S(p)=\{s: p \in L(s)\}$

Our ultimate goal is to develop an efficient algorithm that operates on [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) to perform ([CTL](temporal%20logic.md) ) [Model-checking](Model-checking.md).

The key step: a fixpoint characterization of temporal modalities.

Some preliminaries:
- $\tau: Powerset(S) \to Powerset(S)$
	$S$ is the set of states
We want to find fixpoints. Lets for instance consider a subset of $S$ we call $S'$ i.e. $S'\in S$ a fixpoint is a subset for which the following holds:
$$\tau(S')=S'$$
The set of states that satisfy a given [CTL](temporal%20logic.md) formula will be characterized  as the least/greatest fixpoint of an appropriate function.

Identifying a function based on its [[fix point]] is called [fix point characterization](fix%20point.md).

Let us define a [Kripke structure](Kripke%20structure.md) $M=(S,R,L)$.

The $Powerset(S)$ can be viewed as a [[lattice]] under the standard set inclusion ordering.

The highest value is when the all states are true. The lowest value is when all states are false. [Power set](Power%20set.md).

![](Verification%2037_image_18.png)

We consider a predicate Transformer:

$$\tau: Powerset(S) \to Powerset(S)$$
What is a predicate in our setting? It is the set of states where the predicate is $true$.

### 2.4.5 General Notions and results
1. [monotonicity](monotone%20functions.md)
	$\tau$ i [monotonic](monotone%20functions.md) if when we have two sets $P$ and $Q$ and $P$ is a subset of $Q$ it implies that also $\tau(P) \subseteq \tau(Q)$ i.e.
	$$P \subseteq Q \implies \tau(P) \subseteq (Q)$$
2. $\tau$ is [[Union Continous]] if when we have a set of states with the following feature: $$P_1 \subseteq P_2 \subseteq P_3 \dots $$
	The following holds: 
	$$\tau(\bigcup_i P_i)=\bigcup _i(\tau(P_i))$$
3. Is [[Intersection Continous]] if when we have a set of states with the following feature: $$\dots P_3 \subseteq P_2 \subseteq P_1$$
	The following holds: 
	$$\tau(\bigcap_i P_i)=\bigcap _i(\tau(P_i))$$
4. We write $\tau^i(z)$ to denote $i$ applications of $\tau$ to $z$ i.e. $\tau^3(z)\equiv \tau(\tau(\tau(z)))$ we have a special case $\tau^0(z)=z$

From torsky we now that a [monotone](monotone%20functions.md) predicate transformer $\tau$ on $powerset(S)$  has at least two [fix point](fix%20point.md)s.
The least [fix point](fix%20point.md):
	$\mu z.\tau z=\bigcap\{z:\tau(z) \subset(z)\}$ 
And the greates fixpoint:
	$vz.\tau z = \bigcup\{z:\tau(z) \subset(z)\}$

If $\tau$ isalso [Union Continous](Union%20Continous.md) then one can represent the least [fix point](fix%20point.md) as:
$$\mu z.\tau z= \bigcup_i \tau^i(false)$$

This is usefull as it tell us that we can reach the least fixpoint by starting from the bottom of the lattice i.e. $false$ and repeatedly applying $\tau$.

As $S$ is finite this operation will terminate at some point.


The general characterization if $\tau$  is [monotonic](monotone%20functions.md) is the following:
$$vz.\tau z=\bigcup_i\{z: z \subseteq \tau(z)\}$$

But whenever $\tau$ is also [Intersection Continous](Intersection%20Continous.md)  then

$$vz.\tau z=\bigcap_i \tau^i(true)$$

We will see that when we have ==existential temporal modality== then we have to move bottom up i.e. starting from false.

When we have ==universal temporal modality== we will move top down i.e. starting from $true$.

---
40 a

---

### 2.4.6 Finite [Kripke structure](Kripke%20structure.md).

>[!Note] [[Lemma 16]]
>If the predicate transformer $\tau$ is [monotone](monotone%20functions.md) and the set of states $S$ is finite, then $\tau$ is also [Union Continous](Union%20Continous.md) and [Intersection Continous](Intersection%20Continous.md).

Proof in Clark book

>[!Note] [[Lemma 17]]
>If $\tau$ is [monotone](monotone%20functions.md) for every index $i$, $\tau^i(false)\subseteq \tau^{i+1}(false)$ and $\tau^{i+1}(true) \subseteq \tau^{i}$ 

>[!Note] [[Lemma 18]]  
>If $\tau$ is [monotone](monotone%20functions.md) and the set of states $S$ is finite, then there exists an integer $i_0$ such that for all $j>i_0$, $\tau^j(false)=\tau^{i_0}(false)$ and the same holds for $\tau^j(true)=\tau^{i_0}(true)$

>[!Note] [[Lemma 19]]
>If $\tau$ is [monotone](monotone%20functions.md) and the set of states $S$ is finite, then there exists an integer $i_0$ such that the least fixpoint  is equal to $\tau^{i_0}(false)$ i.e. ($\mu z.\tau z=\tau^{i_0}(false)$) and there exists an integer $j_0$ such that the greates fixpoint $v z.\tau z$ is equal to $\tau^{i_0}(true)$ i.e. ($v z.\tau z=\tau^{j_0}(true)$)

There is even a maximum runtime. The number of maximum applications of $\tau$ is equal to the [Cardinality](Cardinality.md) of $S$ i.e. $|S|$.

An algorithm for computing the greatest/least fixpoint of such a $\tau$ can be easily be written:

 We will denote them as $lfp$ and $gfp$ respectively to find the **l**east **f**ix **p**oint and the **g**reates **f**ix **p**oint.

Lets start with $lfp$
$lfp(\tau: \text{ predicate transformation}): \text{ predicate}$

it takes in a predicate transformation and returns a predicate.

>[!Reminder] 
>A predicate is a set of states which contains the states in which the predicate is  true.

```
Q:=false
Q':= tau(false)
while (Q' != Q) do:
	Q=Q'
	Q'= tau(Q')

return Q
```

Now lets go on with $gfp(\tau: \text{ predicate transformation}): \text{ predicate}$

```
Q:=true
Q':= tau(true)
while (Q' != Q) do:
	Q=Q'
	Q'= tau(Q')

return Q
```


The invariance of the while loop  is given by the following assertion: $Q'=\tau(Q) \land Q' \subseteq \mu z.\tau z$.

It is easy to check  that at the beginning of the $i^{th}$ iteration $Q=\tau^{i-1}(false)$ and $Q'=\tau^i(false)$

By [Lemma 17](Lemma%2017.md) we have that $false \subseteq \tau(false) \subseteq \tau^2(false) \subseteq \dots$

Then the maximum number of iterations, as at each step we can only increase or keep the [Cardinality](Cardinality.md) of the set in the last iteratation is at most the number of states.

When the loop terminates we will have that $Q=\tau(Q)=Q'$ which is the termination condition.

Also when we remember the definitioin of a [fix point](fix%20point.md) i.e. $X=f(X)$ we see that at that point $Q$ is a [fix point](fix%20point.md) of $\tau$ i.e. $Q=\tau(Q)$. By the definition of the least [fix point](fix%20point.md) ($\mu z.\tau z$) must be included in all other [fix point](fix%20point.md)s from there it follows that $\mu z.\tau z \subseteq Q$.

This allows us to conclude that $Q$ is exactly the least fixpoint i.e. $\mu z.\tau z = Q$

The very same argument holds for the greatest fix point.


## 2.5 What does all of this now have to do with [CTL](temporal%20logic.md)?

A characterization of [CTL](temporal%20logic.md)  modalities as least fixpoint and greates fixpoint of suitable predicate transformers.

$A(F(f_1))=\mu z.f_1 \lor A(X(z))$

This formula says that for all states there exists a state where at some point $f_1$ is true. This is the same as that either $f_1$ is true now or for all successors $z$ is true.

$E(F(f_1))=\mu z.f_1 \lor E(X(z))$
$A(G(f_1))=vz.f_1 \land A(X(z))$
$E(G(f_1))=vz.f_1 \land E(X(z))$
$A((f_1)U(f_2))=\mu z.f_2 \lor (f_1 \land A(X(z)))$
$E((f_1)U(f_2))=\mu z.f_2 \lor (f_1 \land E(X(z)))$

>[!Syntax]
>What does the syntax $\mu z.f_2$ mean it is the least fixpoint of the function $f_2$ on the set of states.

There is one general rule:
The state quantifier defines if we use the least or the greates fixpoint:
- $F$ -> $\mu z$ i.e. least fixpoint
- $G$ ->$vz$ i.e. greates fixpoint
- $U$ -> mixed


==Lets proof==
>[!Remember]
>Each [CTL](temporal%20logic.md) formula is can be identified by the set of states where the formula is true.

>[!Remember]
>$\tau: Powerset(S) \to Powerset(S)$
>Meaning it takes as input a subset of $S$ (or $S$ itself) and returns a subset of $S$ (or $S$ itself) 

Let us first focus on:
$$E(G(f_1))=vz.f_1 \land E(X(z))$$

Proof 1:
$\tau(z)=f_1 \land E(X(z))$ is monotonic

Let $P_1 \subseteq P_2$. We have to show that $\tau(P_1) \subseteq \tau(P_2)$

Let $s \in \tau(P_1)$ that is $s \in f_1 \land E(X(P_1))$

For $\tau(P_1)$ to be true $s$ needs to make $f_1$ and ($\land$) $E(X(P_1))$ true i.e. $s \models f_1$ and the second thing this implies that there exists a state $s'$ after $s$. This can be also be written as $R(s,s')$ which reads as $s'$ is a successor of $s$ via $R$). such that $s'$ belongs to $P_1$

Lets exploit now the hypothesis that $P_1 \in P_2$.
Since $P_1$ is a subset of $P_2$ it follows that $s'$ also belongs to $P_2$ and thus we have that $s\in \tau(P_2)=f_1 \land E(X(P_2))$ . All of this follows from the monotonicity of $\tau$
$\square$


>[!Note] [Lemma 20](Lemma%2020.md)
>let $\tau=f_1 \land E(X(z))$ and $\tau^{i_0}(true)$ be the limit of the sequence $\dots \subseteq \tau(\tau(true)) \subseteq \tau^0{true} \subseteq true$.
>Now for every state $s \in S$ if $s \in \tau^{i_0}(true)$ then $s \models f_1$ and there exists a state $s'$ such that we can go from $s$ to $s'$ i.e. $R(s,s')$ is true and $s' \in \tau^{i_0}(true)$


>[!Note] [[Lemma 21]]
>$E(G(f_1))$ is a fixpoint of the function $\tau(z)=f_1\land E(X(z))$

>[!Note] [[Lemma 22]]
>$E(G(f_1))$ is the greates [fix point](fix%20point.md) of $\tau(z)=f_1\land E(X(z))$


==Example==
We have a [Kripke structure](Kripke%20structure.md).

  The question we have is: Where is our formula: $E(G(P))$ true?

We can express our formula through a fixpoint:
$$E(G(P))=vz.p \land E(X(z))$$

![](Verification%2037_image_19.png)


As we can see the formula is never $true$ as all paths end up in $s_4$ where $p$ is $false$.

That means our algorithm should return the empty set.

>[!Note] how do we read the formula $E(G(f_1))=vz.f_1 \land E(X(z))$
>In this case $f_1$ is a nested logical function on the [Kripke structure](Kripke%20structure.md) i.e. starting from all states.
>$z$ on the other hand is the argument of the function i.e. $\tau(z)=f_1 \land(E(X(z)))$. $f_1$ could for instance be $p$ or another logical function $p \land \neg q$. See the example below to see what the difference between $f_1$ and $z$ is applied.


1. We start with $\tau(true)$ 
	This is equivalent to $\tau(\{s_0,s_1,s_2,s_3,s_4,s_5\})$
	Lets now evaluate it. The first three states that we can add to our result are $\{s_1,s_2,s_3\}$ as $p$ is true in this states and so the formula $p \land E(X(z))$ evaluates $true$ for sure. The next question is now which of the remaining states makes $E(X(z))$ $true$. Here $z$ is the set of states that we initially put into the calculation i.e. $\{s_0,s_1,s_2,s_3,s_4\}$. The formula $E(X(z))$ asks which of them has a successor in the set $z$. As every node as ha successor, the result is: $E(X(z))=\{s_0,s_1,s_2,s_3,s_4\}$.
	
	This results in the following formula:
	$$vz.p \land E(X(z))=\underbrace{\{s_1,s_2,s_3\}}_{p} \land \underbrace{\{s_0,s_1,s_2,s_3,s_4\}}_{E(X(z))}=\{s_1,s_2,s_3\}$$
2. Schritt $\tau^2(true)=\tau(\{s_1,s_2,s_3\})$
	$p$ stays always the same, but the argument $z$ has now been reduced to only three states i.e. $\{s_1,s_2,s_3\}$.
	$$vz.p \land E(X(z))=\underbrace{\{s_1,s_2,s_3\}}_{p} \land \underbrace{\{s_1,s_2\}}_{E(X(z))}=\{s_1,s_2\}$$
	$E(X(z))$ looses $\{s_3\}$ as it does not have a successor.
3. Schritt bis n-ter schritt
	The set $E(X(z))$ always looses one more set till it does not have elements any more after a couple of iterations we have:
	$$vz.p \land E(X(z))=\underbrace{\{s_1,s_2,s_3\}}_{p} \land \underbrace{\{\}}_{E(X(z))}=\{\}$$


Lets change the tree a bit to see if we can let the algorithm return a non-empty set. Therefore we add a self loop to $s_3$.

![](Verification%2037_image_20.png)

Now we can see that $E(G(p))$ is true for the path $s_3^\omega$, as this path always has one successor where $p$ is always true.

And indeed the formula converges to the following:
$$vz.p \land E(X(z))=\underbrace{\{s_1,s_2,s_3\}}_{p} \land \underbrace{\{s_3\}}_{E(X(z))}=\{s_3\}$$
>[!Note] [[Lemma 23]]
>In the case of the existential quantifier: $E((f_1)U(f_2))$ is the least fixpoint of the predicate transformer $\tau(z)=f_2 \lor(f_2 \land E(X(z)))$
>

We skip the proof.

==Example==

We start from the empty set i.e. $\tau(false)=\{\}$

We want to compute $E((p)U(q))$ on the following structure:

![](Verification%2037_image_21.png)

We first create our function following [Lemma 23](Lemma%2023.md): 
$\tau(z)=q \lor (p \land (E(X(z))))$

1. step
$\tau(false)=q \land p \land E(X(\emptyset))=$
$=\{s_2\}\lor \{s_0,s_1\} \land \emptyset=\{s_2\}$

2. step
$\tau(\{s_2\})=q \land p \land E(X(\{s_2\}))=$
$=\{s_2\}\lor \{s_0,s_1\} \land \{s_1,s_3\}=\{s_2,s_1\}$

3. step
$\tau(\{s_1,s_2\})=q \land p \land E(X(\{s_1,s_2\}))=$
$=\{s_2\}\lor \{s_0,s_1\} \land \{s_0,s_1,s_2,s_3\}=\{s_0,s_1,s_2\}$

4. step
	$\tau(\{s_0,s_1,s_2\})=q \land p \land E(X(\{s_0,s_1,s_2\}))=$
	$=\{s_2\}\lor \{s_0,s_1\} \land \{s_0,s_1,s_2,s_3\}=\{s_0,s_1,s_2\}$
We see that in the fourth step the resulting set stays the same i.e. we have found a [fix point](fix%20point.md).


We are now ready for symbolic model checking.
# 3 Preliminary steps to [Symbolic model-checking](Symbolic%20model-checking.md): [QBF](QBF.md)

[[QBF]] does not increase the [expressiveness](expressiveness) of boolean formulas, but it allows in many cases to write more [Succinct](Succinctness.md) formulas.


What happens if we want to use [Shannon-Expansion](Shannon-Expansion.md) in [QBF](QBF.md)

$\exists x f =f|_{x \leftarrow 0} \lor f|_{x \leftarrow 1}$

$\forall x f =f|_{x \leftarrow 0} \land f|_{x \leftarrow 1}$

We will make use of the following expressions:

$\exists \vec{v}(f(\vec{v},\vec{w}) \land g(\vec{v},\vec{x}))$

This symbolic [Model-checking](Model-checking.md) algorithm called $CHECK$ takes as input a [CTL](temporal%20logic.md) formula and a [Kripke structure](Kripke%20structure.md) structure and returns as output a [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) that represents the set of states where the formula is true.

# 4 CHECK
$CHECK$ is inductively defined on the structure of the formula.

- if $f$ is a [Propositional Letter](Propositional%20Logic) then $CHECK(f)$ returns the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for such a letter.
- if $f$ is $f_1 \land f_2$ or $\neg f_1$, we just apply the algorithm $APPLY$ to the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $f_1$ and  $f_2$
- The only complex case we have to consider  are the ones containing temporal modalities which are
	- $\underbrace{E(X(f_1)),E((f_1)U(f_2))}_{existential}$ and $\underbrace{E(G(f_2)}_{universal}$
	- 