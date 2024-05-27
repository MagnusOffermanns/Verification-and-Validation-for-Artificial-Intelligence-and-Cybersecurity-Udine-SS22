# 1 [[Synthesis Problem]]
I It consists of the synthesis of a finite state machine (a circuit) which realizes a bit-to-bit transformation of an infinite sequence $\alpha$
into a corresponding infinite sequence β so that the pair $(\alpha, \beta)$  satisfies a specification expressed in a suitable (temporal) logic.

satisfies a specification expressed in a suitable (temporal) logic.
**Goal**: given a specification of the input-output relation between α

$\alpha,\beta$ are two binary strings we want to, build a corresponding machine (or blackbox shown as $?$)that converts $\alpha$ into $\beta$ using a certain rule. For instance the negation of all bits as in the following example:

![](Verification%2043_image_1.png)

>[!Note] 
>In this class we work with finite strings

==Example==

==First Condition==
$$\forall t(\alpha(t)= 1 \to \beta(t)=1)$$

If at a given time $t$ the input is 1 the output should be $1$ as well.

For instance one solution to this specification would be a constantly blackbox that always returns $1$.

So lets add a **second condition** to prevent the easy solution before:

$\neg \exists t ( \beta(t)=\beta(t+1)=0)$

This says that there should not be 2 consecutive $0$ in the output sequence

Now lets add a **third Condition**:

$\exists^\omega t (\alpha(t)=0 \to \exists ^\omega t \beta(t)=0)$
If the input sequence contains an infinite number of $0$, then the output should also have an infinite number of 0 as well.

**What is a solution?:**
- When there is a 0 we return 0
- if the input is 0, it produces the output 1 if the previous output was a 0, otherwise it returns 0.

What other conditions need to be satisfied?

1. **bit-to-bit**  
	When the machine receives the $n_{th}$ character of $α$ (as input), it must immediately produce the $n-th$ character of $\beta$ (as output). It follows that $\beta(n)$ may only depend on $\alpha(1),\dots , \alpha(n − 1), \alpha(n)$; i.e. no output delay...
2. **a finite state solution (machine)**
	 To compute the output of a generic computation step (the output at time $t$), the machine needs to exploit a finite memory of a given size.

A possible solution is the following automaton:

![](Verification%2043_image_2.png)

>[!Question]
> What does the syntax of $x/y$ over the edges mean?
> $x$ is the ingested letter, $y$ is the output letter.
> so if we are in state "last output 0" and we ingests $0$ or $1$ we go to the state "last output 1" and output $1$.



==Example 2==
 $\beta(t) = \alpha(2t)$
 <mark style="background: #FF5582A6;">This is not possible</mark> We need information from the future!
($\beta$ returns the elements at even positions of $\alpha$)
violates condition 1 **bit-to-bit** – the output symbol $\beta(t)$ must be produced without delay after receipt of the input symbol $\alpha(t)$;

==Example 3==
$\beta(2t)=\beta(2t+1)=\alpha(t)$
<mark style="background: #FF5582A6;">This is not possible</mark> as the number of elements we need to save increases with $t$. That is because the input of $\alpha$ lags 1 behind each timestep, meaning that we need to save one additional output of $\beta$ each timestep. This is because we have to fullfill the **bit-to-bit** condition.

![](Verification%2043_image_3.png)

 ($\beta$ “doubles” the position of each symbol of $\alpha$) violates condition 2 **a finite state solution (machine)** – we need to record an unboundedly increasing number of symbols for future use;

==Example 3==
 $β = 111 . . .$, if $α$ features an infinite number of occurrences of 1; otherwise, $β = 000 \dots$ 
 violates condition 1 as well – the first symbol of the output sequence β cannot be determined on the basis of any finite prefix of α. i.e. if we saw already $n$ $1$s it is not sure that there will not be a $0$ in the future.

## 1.1 [[Mealy automaton]] aka [input-output automaton](Mealy%20automaton.md).

A [Mealy automaton](Mealy%20automaton.md) $\mathbb{M}$ is:
- a finite state automaton
- with an output function:
	$\tau: S \times \Sigma \to \Gamma$
	- $S$ is the finite set of states
	- $\Sigma$ is a finite input alphabet
	- $\Gamma$ is a finite output alphabet

Given the input sequence:
$$\alpha=\alpha(1),\alpha(2),\dots$$
The output sequence can be denoted as:
$\mathbb{M}=\beta=\beta(1),\beta(2),\dots$

where $\beta(t)$ is calculated by using the output function $\tau$
$$\beta(t)=\tau(\underbrace{\delta^*(s_0,\alpha(0),\dots,\alpha(t-1))}_{\text{defines the current state}},\underbrace{\alpha(t)}_{\text{next transtions}})$$

![](Verification%2043_image_4.png)

- $\delta^*(s_0,\alpha(0),\dots,\alpha(t-1))$
	here is needed to define the current state of the automation. Starting from $s_0$ we input the symbols $\alpha(0)$ till $\alpha(t-1)$ till we are in a certain state for instance $s_x$
- $\alpha(t)$
	Is the symbol ingested last to go from the state reached in $t-1$ i.e. $s_x$ to the next state $s_y$ i.e. the state when we are in state $s_x$ and ingest the symbol $\alpha(t)$


## 1.2 Specification
Initially the researchers defining [Mealy automaton](Mealy%20automaton.md) based their reasoning on [S1S](Monadic%20second%20order%20of%20one%20sucessor.md): [Monadic second order of one sucessor](Monadic%20second%20order%20of%20one%20sucessor.md) denoted by $(w,+1)$

- The ordering relation $<$ is (second-order) definable in terms of the successor function $+1: s < t$ if and only if t belongs to each set that includes $s + 1$ and is closed under successor relation.
- I For the sake of simplicity, we will only consider Boolean input and output alphabets, that is, $\{0, 1\}$.
-  The [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)-formulas $φ(X, Y)$ we will take into consideration talk about sequences $α \in {0, 1}^\omega$ and $β ∈ {0, 1}^\omega$. 
- The free variable $X$ identifies those positions where $α$ takes value $1$, while the free variable $Y$ identifies those where $β$ takes value 1. We denote the interpretations of $X$ and $Y$ induced by $α$ and $β$ by $P_\alpha$ and $P_\beta$ , respectively. That means that $P_\alpha$ and $P_\beta$ are predicates that when given a timepoint $t$ they return $true$ if at that position $\alpha$ or $\beta$ are $1$.
![](Verification%2043_image_5.png)


## 1.3 [[Church's Problem]]
Church’s problem can be precisely stated as follows:

Given an [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)-formula φ(X, Y), build a Mealy automaton M, with input alphabet $\Sigma = \{0, 1\}$ and output alphabet $\Gamma = \{0, 1\}$, such that, for every input sequence $α ∈ \{0, 1\}^\omega$ ,the [Mealy automaton](Mealy%20automaton.md) $\mathbb{M}$ generates an output sequence $β ∈ {0, 1}^\omega$ such that $(w,1)\models \varphi[P_\alpha,P_\beta]$ (or it answers that such an automaton does not exist).

It can be easily generalized to an input alphabet $\Sigma = \{0, 1\}^{m_1}$ and/or to an output alphabet $\Gamma = \{0, 1\}^{m_2}$.

A **finite state winning strategy for an infinite game**: according to a game-theoretic interpretation, a [Mealy automaton](Mealy%20automaton.md) can be viewed as the definition of a **winning strategy** for player $B/β (Bob)$ that replies to the moves of player $A/α (Alice)$.


---
VV 44 b

---

# 2 Turning a [Automaton](Deterministic%20Finite%20State%20Automata.md) into a game
We know all the features from above already. The thing we will learn is how to turn a [Automaton](Deterministic%20Finite%20State%20Automata.md) into a game.

## 2.1 The soultion of Büchi-landweber

They first write a [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula then transform it into a Deterministic [Muller Automata](Muller%20Automata.md). Then it gets transformed into a [[Muller Game]] and then into a [[parity game]].


![](Verification%2043_image_6.png)

## 2.2 From [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) to [Muller Game](Muller%20Game.md)
We first transform a [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) specification into a deterministic [Muller Automata](Muller%20Automata.md).

We know that

$$S1S \equiv NBA \equiv DMA$$
$NBA$ = Nondeterministic [Buechi automata](Buechi%20automata.md)
$DMA$= [Deterministic Muller Automata](Muller%20Automata.md)

We can transforms are computable but **extremely expensive.**

Therefore lets look at a solution:

## 2.3 From [Muller Automata](Muller%20Automata.md) to [Muller Game](Muller%20Game.md)
The automaton in the previous step is transformed into a game.

==Lets do an example==

We have the following [Muller Automata](Muller%20Automata.md) which fullfills the above mentioned specifications and we want to turn it to a [Muller Game](Muller%20Game.md).

![](Muller%20Game_image_1.png)

Each State $A_x$ is split up into multiple nodes,  node that is controlled by the adversary (Alice) and into some states controlled by us $(A_x,1)$ or $(A_x,0)$ colored **green**. This means that if we are in a adversary node (All $A$ nodes colored **orange**) the adversary can choose which path to take. The path taken is the input bit. If we are in a state controlled by us, i.e. the **green** nodes, we can choose what path we want to take. This is the output bit.

In the example below we see the split up of the node $A_0$, which splits up into the node $(A_0,0)$ controlled by us and the node $(A_0,1)$ controlled by us. So depending on the input bit the adversary choose either to go to $(A_0,1)$ or $(A_1,0)$. Then we the player chooses an output bit going to $A_1$ or $A_2$ (from $(A_0,0)$) or $A_3$ or $A_4$ (from $(A_0,1)$)). 

This models the dynamic that the adversary controls the input bits, us the player control the output bits.

After the input bit was choosen by the adversary, and the output bit is chosen by us, we return to a existing node of the $A$ states. In the picture below$A_0$ is one state, while $A_1$ till $A_4$ might be all distinct states or might be the same one as for instance when we convert the [Muller Automata](Muller%20Automata.md) from above turn into a [Muller Game](Muller%20Game.md).

![](Verification%2043_image_8.png)

Lets now convert the [Muller Automata](Muller%20Automata.md) from above into a [Muller Game](Muller%20Game.md):

![](Muller%20Game_image_1.png)

Below we see the converted [Muller Game](Muller%20Game.md). The square states are controlled by the adversary, the round states are controlled by us.

>[!Note] 
>The nodes have different names
>$A_0 \equiv 1$
>$A_1 \equiv 3$
>$A_2 \equiv 6$

Lets see how we create all branches from the state $1$.
From the state $1$ i.e. $A_0$ we have four outgoing branches. Where $p$ is is the input bit, and $q$ is the output bit. 

$(p,q)$
$(1,1)$
$(1,0)$
$(0,1)$
$(0,0)$

That means the adversary has two choices either he chooses $0$ or $1$. For both choices we create a node. Node $2$ for the choice of $1$ and Node 4 for the choice of 0.

Now we have to look where the outgoing branches go for Node $2$. If the output is $0$ i.e. $(1,0)$ we go in the automaton to state $A_2$ i.e. Node $6$. If the output (i.e. we control the output)is $1$ we stay in the same state $A_0$ i.e. node $1$.

With that we have the following game.

![](Verification%2043_image_9.png)

Now lets add the node if the input is $0$. We therefore create a Node $4$. Then when the output is $1$ we go back to $A_0$ i.e. Node 1. If the output is $0$ we go to state $A_1$ i.e. Node $3$. This leads to the following game tree:

![](Verification%2043_image_10.png)

This are all branches for for node 1. Then we continue with node $3$ and node $6$. This results in the following graph.

![](Muller%20Game_image_2.png)

## 2.4 Games on the [Muller Game](Muller%20Game.md) arena

We now introduce different games and the winning condition for games on the game graph of [Muller arenas](Muller%20Game.md)s.

### 2.4.1 Game graph 
Is the board on which we play the [Muller Game](Muller%20Game.md).

the Graph has the following setup:
- $Q$: All states
- $Q_A$: States controlled by the adverary
- $Q_B$: States controlled by the player
- $E$ -> edges
There are no deadlocks: i.e. $\forall q \in Q: Eq \neq \emptyset$

Each edge from $Q_A$ goest to a state in $Q_B$ and vice-versa.

 A play on the game graph $G$ from $q$ is an infinite path $ρ$ on $G$ with initial state $q$ (infinite games). We assume $A$ to choose the next state when we
are in a $Q_A$ state and b to choose it when we are in a $Q_B$ state.

 A game is a pair $(G, W)$, where $G = (Q,Q_A,Q_B E)$ is a game graph and $W \subseteq Q^\omega$ is the set of winning conditions for player B.


  Player B wins the play if he can create a path through the arena $G$ $\rho = q0,q1,q2 \dots$ that is part of the set of winning conditions i.e. $\rho ∈ W$. If he can not force a path that is part of the winning condition A wins.
We are interested in finitely definable winning conditions.

## 2.5 [Muller Game](Muller%20Game.md)s, [Weak muller game](Muller%20Game.md)s and Reachability games

### 2.5.1 [Muller Game](Muller%20Game.md)s winning condition
- [Muller Game](Muller%20Game.md)
	 Muller games: the winning condition is a collection of sets of states $F ⊆ 2^Q$ such that $B$ wins $\rho$ if and only if $Inf(ρ) ∈ F$. That is simmilar to the original [Muller Automata](Muller%20Automata.md) acceptance condition
- [Weak muller game](Muller%20Game.md)s
	There exists a weak version of the winning condition of Muller games (Staiger-Wagner condition), according to which $B$ wins the play $ρ$ if and only if $Occ(ρ) ∈ F$, where $Occ(\rho) = {q \in Q : \exists i(\rho(i) = q})$. That means that we do not have to traverse a state $p$ infinitely many times, but $p$ only needs to be traversed once.
- [Reachability Games](Muller%20Game.md)
	We define a set of winning sates $F \in Q$. $B$ wins the play $\rho$ if some state in the play belongs to $F$.


## 2.6 Strategies, [Winning Strategy](Strategy.md) and determined games.

- A [Strategy](Strategy.md) for a player is a mapping $f : Q^+ \to Q$ such that, given the history of the game up a certain state (under his/her control), specifies his/her behavior at the next step.
-  A strategy $f$ for player $B$ from $q$ is a [winning strategy](Strategy.md) if each play from $q$, played according to f , is won by player B.
- [winning region](Strategy.md) 
	$WB := \{q \in Q | B \text{wins starting from} q\}$ is said the winning region of $B$ (the same for $A$). 
- Obviously, the winning regions of Alice and Bob can not be overlapping $WA \cap WB = \emptyset$.
- [Determined games](Strategy.md)
	If $W_A \bigcup W_B=Q$   we say that the game is a determined game. This means that for each state of the game, one of the two players have a [winning strategy](Strategy.md).


## 2.7 What is the solution of a Game?
The [[solution of a game]] $(G,W)$ and $G=\{Q,Q_A,E\}$ and $W$ finitely describable, consists of two steps:
1. to establish for each $q \in Q$ if $q \in W_A$ or $q\in W_B$
2.  to build a (finitely describable) winning strategy starting from gamestate $q$ (for $B$, if $q \in W_B$ ; for $A$, otherwise).

There are two types of [Strategies](Strategy.md):
- positional Strategy:
	A strategy is positional if the value of $f(q_1,\dots,q_k)$ only depends **on the current state $q_k$**. A positional strategy for $B$ is a mapping $f: Q_B \to Q$ (similarly for $A$)
 In graph-theoretic terms, a positional strategy for $B$ can be expressed as a subset of edges of $G$, which includes all edges exiting from states in $Q_A$ and at least one edge exiting from states in $Q_B$ (the one identified by the function).
This means that independently how the player $A$ plays in one of the states in $Q_A$, we can react with one distinct move when it is our turn i.e. we are in one of the states in $Q_B$

# 3 Finite State strategies and Computed Strategies
In easy words it means that **we can build a finite state [Mealy automaton](Mealy%20automaton.md) that tells us how to win the game.**

-  Formally, $f$ is a finite state strategy if it can be computed by a Mealy automaton of the form $S = (S, Q, Q, s_0 , \delta, \tau )$ , where $S$ is a finite set of states, $Q$ is both the input and output alphabet, $s_0 \in S$ is the initial state, $\delta : S \times Q \to S$, and $\tau : S \times Q_A \to Q$, for $A$, and $\tau : S \times Q_B → Q$, for $B$.


- $\delta$ is the transitions function telling us how we move in the [Mealy automaton](Mealy%20automaton.md).
- $\tau$ are the transition functions defining to which state we need to go depending on the current state of the game $Q_A$ or $Q_B$ and the state of the [Mealy automaton](Mealy%20automaton.md) $S$.


- A strategy $f : Q^+ \to Q$ on a finite set of states $Q$ can be viewed as a function on words.

A strategy  $f_S$ **computed** by an [Mealy automaton](Mealy%20automaton.md) $S$  can be defined by a function:

$$f_S(q_0,\dots,q_k)=\tau(\underbrace{\delta^*(s_0,q_0 \dots q_k-1)}_{\text{state at } k},\underbrace{q_k}_{\text{input at position  } k})$$

where $\delta^*(s,w)$ is the state reached by $S$ starting from position $s$ on the input word $w$ and $\tau$ is chosen by the player who is responsible for $q_k$


>[!Note] [[Theorem 24]] 
>[Weak muller game](Muller%20Game.md)s are [Determined](Strategy.md) and for each weak [Muller Game](Muller%20Game.md) $(G, F)$, where $G$ has $n$ states, the winning regions for the two players can be effectively determined and it is possible to build, for each state $q$ in $G$, a [Finite state winning strategy](Strategy.md)  from $q$ (for the winning player) making use of a memory with $2^n$ states.

The explanation of the memory of the [Mealy automaton](Mealy%20automaton.md) needed for the finite state winning strategy is because of the winning condition of [Weak muller game](Muller%20Game.md). We need to encounter one of the final states.

The number $2^n$ is the number of subsets that can be created from $n$ states, which represents the notion of going into every state at least once.

>[!Note] [[Theorem 25]] 
>[Muller Games](Muller%20Game.md) are [Determined](Strategy.md) and for each Muller game $(G, F)$, where $G$ has $n$ states, the winning regions for the two players can be effectively determined and it is possible to build, for each state $q$ in $G$, a finite state winning strategy from $q$ (for the winning player) making use of a memory with $n! \cdot n$ states.


# 4 A solution of [Church's Problem](Church's%20Problem.md)

1. given [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula $\varphi(X,Y)$ we transform it into a [Muller Automaton](Muller%20Automata.md) $M$
2. We transform the [Muller Automata](Muller%20Automata.md) into a [Muller Game](Muller%20Game.md) with graph $G$ and Muller Winning condition ($G$ inherits its initial state from the automaton)
3.  [Buechi Landweber Theorem](Theorem%2025.md) makes it possible to determine the winning regions and to establish whether the initial state of the game belongs to $W_B$ ; in such a case, we build the [Mealy automaton](Mealy%20automaton.md) $S$ which realizes the winning strategy, starting from the initial state ($S$ is called the strategy automaton);
4. the [Mealy automaton](Mealy%20automaton.md) $A$, that solves [Church's Problem](Church's%20Problem.md), is obtained from the product of the strategy automaton $S$ and the game graph $M$.

It is worth pointing out that [Buechi Landweber Theorem](Theorem%2025.md) is exploited only at step 3.



## 4.1 Step 4 in detail
1. The state space of $A$ is $Q \times S$, where $Q$ is the set of states of the [Muller Automaton](Muller%20Automata.md) $M$ and $S$ is the set of states of the strategy automaton $S$, and its initial state is $(q_0 , s_0 )$;

2. A transition (of the [Mealy automaton](Mealy%20automaton.md)) must be specified for each state $(q, s)$ and each input bit $b$, that is, an output bit $b'$ and a new  state $(q' , s' )$; 

3. To this end, the state $q^∗ = (q, b)$ of the game graph $G$ and the state $s^* = \delta(s, q^∗ )$ of the strategy automaton $S$ associated with it must be computed;

4. The output function of $S$ returns the state $q' = \tau(s^* , q^* )$ of the game graph $G$, while its transition function returns the new memory state $s' = \delta(s^* , q_0 )$;

5. the output bit $b_0$ is the value $out(q, b, q_0 )$ associated with the transition from $q^∗ = (q, b)$ to $q'$ .

>[!Note] **Remark**:
> The memory of A combines the state space of the Muller automaton M and the state space of the strategy automaton S (see item 1).


Visually this looks like this:

![](Verification%2043_image_12.png)

1. We are in the in the initial state of the strategy automaton $s_0$
2. The state of the game arena gets announced, we jump from $s_0$ to a state $s$ in which we can react to the new state $q$ (the state of the game arena)
3. The first input bit $b$ is chosen, this makes it necessary that the strategy automaton changes it state depending on the current state of the game arena $q$ and the chosen input bit $b$ this is referred to as $(q,b)=q^*$
4. The strategy automaton changes its state from $s$ to $s^*$ depending on chosen input bit and the game state i.e. $(q,b)=q^*$. This is referred to as an invocation of the transfer function $\delta(s,(q,b))=\delta(s,q^*)=s^*$
5. The output bit $b'$ is chosen by the strategy automaton, resulting in an change on the game graph from state $(q,b)$ to state $q'$. This is an invocation of the transfer function $\tau(s^*,q^*)=q'$ The movement on the game graph has ended.
6. As we are now in a new a new state in the game graph, we have to adapt the state of the strategy graph one last time therefore we consider the state of the game graph and the state of the strategy graph ($\delta(s^*,q')$)resulting in a final state $s'$

# 5 [Reachability Games](Muller%20Game.md)

>[!Note] [[Theorem 26]]
>A [Reachability Games](Muller%20Game.md) $(G, F)$, with $G = (Q, Q_A , E)$ and $F \subseteq Q$, is determined and both the winning regions $W_A$ and $W_B$ for players $A$ and $B$, respectively, and the corresponding [positional strategies](Strategy.md) are computable.

>[!Note] Proof
> For $i = 0, 1,\dots$, compute the vertices starting from which player $B$ can force a visit in $F$ in at most $i$ moves ($i^{th}$ attractor $Attr^i_B (F)$).
> 
> When do we add a state to the set of $Attr_B$? If it is a state under the control of $B$ there needs to be one edge ($\exists$) to a state that is already part of $Attr_B$. If the state is under control of $A$ all ($\forall$) edges need to go to a state that is already part of $Attr_B$.
> 
>The sequence $Attr^0_B (F)(= F) \subseteq Attr^1_B(F) \subseteq Attr^2_B(F) \dots$ becomes It stationary can be easily for some proved index that $k ≤ |Q|$. We define $Attr_B=\bigcup^{|Q|}_{i=0}Attr^i_B(F)$.
> It can easily be prooven that $W_B=Attr_B(F)$.

---
45 a

---

# 6 [Weak muller game](Muller%20Game.md)s

It is possible to show that the winning condition for weak Muller games (player $B$ wins a play $\rho$ if and only if $Occ(\rho) \in F$ (the collection of the states visited by ρ is one of the set in F) can be expressed as **Boolean combinations of reachability conditions**.

In general, positional strategies do not suffice to win [Weak muller game](Muller%20Game.md)s. In some cases, indeed, it is necessary to remember the states that have been already visited.

Lets look at the example for Thomas tutorial:

![](Verification%2043_image_13.png)

**Solution:** a [Mealy automaton](Mealy%20automaton.md) $S$ with the set $Q$ of the states of the game as its input alphabet, the powerset of $Q$ as the set of its states ($2^{|Q|}$
states), and $\emptyset$ as the initial state.
The idea of the appearance record: on the input word $q1,\dots , qk$ , $S$ reaches the state ${q1 , . . . , qk }$  $(\delta(R, p) = R ∪ {p}).$


# 7 [weak parity game](parity%20game.md)s from [Weak muller game](Muller%20Game.md)s

Pairty -> even and odd

It is possible to associate a $number$ (color) $c(R)$ with each $R ⊆ Q$ that codifies two pieces of information: the size of $R$ and the membership
(or not) of $R$ to $F$.

What number do we give each subset?
- If $R \in F$
	$c(R)=2 \cdot |R|$
- if $R \not \in F$
	$c(R)=2 \cdot |R|-1$

Now to determine the cardinality of $R$
We do the following operation:
$$Ceil(c(R)/2)$$
Where $Ceil$ is a rounding up.

To determine the member ship of $R$ to $F$ we check if the number $c(R)$ is even or odd
- even: $R \in F$
- odd: $R \not \in F$

Let $ρ$ be a play and $R_0 , R_1 , R_2 ,\dots$ be the associated sequence of appearance records.

It holds that $Occ(ρ) \in F$ if and only if the maximum color of the sequence $c(R_0), c(R_1 ), c(R_2),\dots$  is even.

A weak Muller game can be transformed into a weak parity game (game simulation).

Lets create an example we have $F=\{\{1,2,3\}\}$ and the following automata:

![](Verification%2043_image_14.png)

$R(\{1,2,3\})=|{1,2,3}|\cdot 2=6$

The cardinality is 3. It does belong to $F$ therefore we do not subtract $1$.

Lets do another example:
$R(\{1,2\})=|{1,2}|\cdot 2-1=3$

The [Cardinality](Cardinality.md) is 2. It does **not** belong to $F$ therefore we do subtract $1$.

If the maximum number $c(R_x)$ is even we win the game i.e. if we only stay in state 1 and 2 i.e. $R(\{1,2\})$  we lose the game as $c(R(\{1,2\}))$ is uneven.
if we traverse all states i.e. $c(R(\{1,2,3\}))$ the number is even, we win the game.

>[!Note] This has multiple advantages
>To look at the game progress one only needs to add the states one traverses in the game, as there is a limited number of states i.e. $|Q|$ the set will not change from a certain point on i.e. a fixpoint is reached. Then we calculate the "color" number. If the number is even we win the game, if the number is uneven we lose the game. We can forget the actual game and only look at the end result. 

We call this game with colors weak parity game.

This introduces the idea of [[Game simulation]].

>[!Note] [Game simulation](Game%20simulation.md)
>When we want to get the result of one game, but play another to deduct the outcome of the first game.

We denote this as as 
$$(G, W) ≤_S (G_0 , W_0 )$$
## 7.1 Consequences of [Game simulation](Game%20simulation.md)s

**Consequence**: positional strategies for $G'$ can be easily transformed into finite state strategies for $G$ (a Mealy automaton). The latter strategies can be realized by automata $S$ enriched with an output function obtained from the positional strategy for $G'$ .

>[!Note] [[Lemma 24]]
>If there exists a [positional winning strategy](Strategy.md)  for player $B$ in $(G' , W' )$ from $(s_0 , q)$, then player $B$ has a [Finite state winning Strategy](Strategy.md) from $q$ in $(G, W)$.

==Proof==
We extend the automaton $S$ with an output function extracted from the winning strategy $σ :Q'_B → Q'$ . To this end, it suffices to define $τ : S × QB → Q$ as $τ (s, q) := π_2 (σ(s, q))$, where $π_2 (σ(s, q))$ is simply the projection on the second component of $σ(s, q)$.


# 8 From [Muller Game](Muller%20Game.md)s to [parity game](parity%20game.md)s 

-  Muller games can be simulated by parity games by means of the [LAR](Latest%20Appearance%20Record.md) ([[Latest Appearance Record]]) structure.
-  Intuitively, a [LAR](Latest%20Appearance%20Record.md) represents the sequence of states encountered during a play, ordered according to their last occurrence / appearance. If the current state was already visited in the past, then it is moved from the position h (called hit) it occupies in the current [LAR](Latest%20Appearance%20Record.md) to the first position of the new [LAR](Latest%20Appearance%20Record.md).

- Given a LAR $((i_1 \dotsi_r ), h)$, its hitting set is the set $\{i1 , ..., ih \}$ of the states which were encountered up to the hit $h$ (including position $h$).

## 8.1 What is a [LAR](Latest%20Appearance%20Record.md)

It is a way to track the states that occur infinitely many times.

We track the occurences of letters, every time we encounter a letter we increase the hitting number. 
1. hitting number $0$
2. hitting number $1$
3. hitting number 2
4. ...

The hitting set contains all letters that we encounter between occurences, ==including the letter itself(as between row 2 and 3, it is only {C})==. Between row 4 and 6 it is for example it is $BD$.

At a certain point the hitting number can not grow beyond a certain value, because there are some states that we just do not encounter anymore.

Then we take the biggest set since the last $n$ steps. The number of last steps is a tuning value.

![](Verification%2043_image_15.png)

We need to run it $n! \cdot n$ this is the number of [LAR](Latest%20Appearance%20Record.md) configurations we can have.

- $n!$ -> all permuations of states
- $n$ -> all values for the hitting time


## 8.2 [parity game](parity%20game.md)s and how we use [LAR](Latest%20Appearance%20Record.md)s to determine the if we won
Let $\rho$ be a sequence over $Q$ and $\rho'$ be the corresponding sequence of [LAR](Latest%20Appearance%20Record.md)s. The set $Inf(\rho)$ coincides with the hitting set $H$ of the maximum hit $h$ that occurs infinitely often in $ρ'$ .

The winning condition for the play $\rho$ of a [Muller Game](Muller%20Game.md) can be reformulated as follows: the hitting set $H$ belongs to the set of final states $F$. 

 The winning condition for [Muller Game](Muller%20Game.md)s can be redefined in terms of a suitable coloring of [LAR](Latest%20Appearance%20Record.md).

==Parity condition==: $B$ wins $\rho'$ if and only if the greatest color that occurs infinitely often in $c(ρ' (0))c(ρ' (1))\dots$ is even.

A colored graph $(G, c)$ with the parity condition is said a [parity game](parity%20game.md).


We run the through the graph while keeping track of reoccurences of nodes using a [LAR](Latest%20Appearance%20Record.md). All unique sets get a colour (number) after the following rule:

![](Verification%2043_image_16.png)

When the biggest set that occures is has a even color (number).

In other words we can say it like this
 
 It can be easily shown that the Muller condition $Inf(ρ) ∈ F$ is satisfied if and only if the parity condition is satisfied:

>[!Note] Proof:
>- if $Inf(ρ) ∈ F$, then $H(= \{i_1 , ..., i_h \}) ∈ F$ and the greatest color that occurs infinitely often is $2h$, which is even.
>-  (⇐) the greatest color that occurs infinitely often is $2h$, which is even, and, thus, the corresponding hitting set belongs to $F$, from which it follows that $Inf(ρ) ∈ F$.


 A [Muller Game](Muller%20Game.md) $(G, F)$ can be simulated by a [parity game](parity%20game.md) $(G' , c)$ by means of a finite state machine that transforms a play $ρ$ on $G$ in a corresponding sequence $ρ'$ of a [LAR](Latest%20Appearance%20Record.md)s (The number of computations of the [LAR](Latest%20Appearance%20Record.md) is $= |Q|! · |Q|$).

## 8.3 [parity game](parity%20game.md)s are deterined

>[!Note] [[Theorem 27]]
>A parity game $(G, c)$ is determined and the construction of the winning regions and the positional strategies for $A$ and $B$ are effective.


Let $Attr_B(S)$ (**attractor** of $B$ for $S$) be the set of states from which $B$ can force in a finite number of steps a visit of a state of $S$.

We look at a [parity game](parity%20game.md):

Let $G=(Q,Q_A,Q_B,E)$ with the coloring $Q -> \{0,\dots,k\}$. We proceed by induction on $|Q|$.

Base case is trivial: If one is already in $S$ one is part of the $attractor$.

Inductive step:
-  Let the greatest color $k$ be even and let $q$ be a state with color $k$.
-  $A_0 = Attr_B (\{q\})$. $Q / A_0$ is a subgame.
	It shows that $B$ can reach the state $q$ in a finite number of steps.
- By the inductive hypothesis, we can partition $Q / A0$ in the two winning region $U_A$ an $U_B$ for $A$ and $B$, respectively. 
	One of the **two cases** holds:
	1.  From $q$, player $B$ can force the play to stay in $U_B \cup A_0$ at the next step.
	- $W_B = U_B \cup A_0$ and $W_A = U_A$ by applying the positional strategies of the inductive hypothesis on $U_A$ and $U_B$ , the attractor strategy on $Attr_B (\{q\})$, and the choice of the next state from $q$ according to Case $1$.
	
	2. From $q$ player $A$ can force the play to stay in $U_A$ at the next step
	- It follows that $q \in Attr_A (U_A)$. Let us consider now the set $A_1 = Attr_A (U_A \cup {q})$. By applying the inductive hypothesis on the subgame induced by $Q / A_1$ , we obtain $V_A$ and $V_B$ . It holds that $W_B = V_B$ and $W_A = V_A \cup A_1$ , where the winning positional strategies are given by the inductive hypothesis and the attractor strategy on $A_1$ .

### 8.3.1 Complexity issues of the creation of winning regions

From the proof of the theorem, it is not difficult to extract a procedure of exponential complexity.

It is known that the problem: “Given a parity game $(G, c)$ and a state $q$, establish whether or not $q$ belongs to the winning region of $B$” belongs
to the complexity class [NP problems](NP%20problems.md) $\cap$ [CO-NP problems](NP%20problems.md).

The possibility of deciding such a problem in [polynomial time](P-Time.md) is one of the most important open problems in the algorithmic theory of infinite games.

>[!Note]  Remark:
>equivalence of the above problem and the model checking problem for the mu-calculus.

A number of variants of [Church's Problem](Church's%20Problem.md) can be obtained by modifying or generalizing the specification language.

A special attention has been given to the synthesis problem for [LTL](temporal%20logic.md) and other [temporal logic](temporal%20logic.md)s.

---
46 a

--











