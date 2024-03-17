# 1 Nondeterministic Planning via Symbolic Model checking


## 1.1 [[Action-based planning]] 

The main issues (partial list):
-  Expressiveness
-  [decideability](decideability.md) and complexity
- Planning as [Satisfiability](Satisfiability.md) checking
- **Planning as [Model-checking](Model-checking.md)**
- Synthesis of plan controllers
- Monitoring of plan execution

The planning problem: finding a sequence of actions that bring a system from an initial state to a goal state, given a set of possible actions (action-based planning).

Elements of the problem:
- Context/Domain:

	- Fluents/variables that describe the considered domain (a.k.a. environment/world)

		-  inertial fluents, whose value can be changed by the execution of some plan action only
		-  non-inertial fluents, whose value can vary independently of the execution of plan actions

	-  States (the set of possible configurations)
	- Actions that cause the transition from a state to the next one
- Initial states
-  Final/goal states


>[!Note] interial variables/fluents
>variables that are influenced by the execution of of our actions

>[!!Note] non-intertial variables/fluents
>variables which influence can change independenlty of the execution of our actions


Sometimes one has [non-inertial fluents](fluents.md). A external condition has to be fullfilled so that a action can be taken.


## 1.2 The standard (restricted) case

- [fluents](fluents.md)/variables take value over finite/discrete domains
- Complete observability
- No external events that may affect plan execution
- Deterministic actions: no uncertainty about the effects of the execution of an action

## 1.3 Nondeterminism
- External events that may cause plan-independent changes in the system
	That means that effects outside of the system influence our planning
- Partial specification of the initial states
	We do not know exactly from which state we begin our execution
- Uncertainty about the effects of actions (nondeterminism)
	We do not know what happens when we take an action, it might lead us to unforseen states.
## 1.4 Extended goal
- properties that the system must satisfy during the execution of the plan, e.g., integrity constraints
	When we have additional constraints of the path planning operation (timely constraints, avoidance of certain states, safety properties etc.)

# 2 Classification of Plans
- [Situated plans](Plans.md)
	The evolution of the plan may be influenced by the environment. Environmental parameters are repeatedly measured, and the selection of the action to execute takes into account such measurements (**trial and error strategies**). One can get stuck in a state and might need to backtrack

- [Universal plans](Plans.md) (A special case of Situated plans)
	Universal plans associate at least one action with any possible state of the domain. In any system configuration, it is thus possible to find a planned action to execute, we never get stuck. We can always act, no **Backtracking**.

- [Conformant Plans](Plans.md)
	In conformant plans, there is no need to collect any piece of information during the execution of the plan in order to achieve the goal. They are useful when observations of the environment are not possible (**null observability**).


# 3 Planning as [Model-checking](Model-checking.md)

The **domain** of the planning problem and its **goal** can be represented by a formal model and a **formula** of a ([temporal](temporal%20logic.md)) logic, respectively.

**The (nondeterministic) planning domain** $(P, S, A, R)$:

- $P$: a finite set of proposition letters $P$ of the form: $fluent_i = value_j$
- $S \subseteq 2^P$ : a finite set of states (a state is defined by the collection of the proposition letters that are true in it, therefore there are also $2^{|P|}$ states)
- $A$: a finite set of actions
- $R \subseteq S \times A \times S$: the transition relation (transition function in case of deterministic planning)

We say that an action a is **enabled** in a state s if there exists a state $s'$ such that $R(s, a, s' )$ i.e. there is a transition from $s$ to $s'$ using the action $a$.


==Example:==
Consider a **parcel** that must transferred from the train station to the airport. The position of the parcel defines both the **initial condition (“at the train station”)** and the **goal (“at the**
**airport”)**.

On the path there **is a traffic light** where the vehicle that transports the parcel has to possibly stop waiting for the green light.

The **color (red or green)** of the traffic light introduces some form of [Non determinism](Non%20deterministic) of the domain (it will be modeled by means of a [non-inertial variable](fluents.md) variable), while the position of the parcel (train station, traffic light, or airport) may only change as the effect of the transportation action ([inertial fluents](fluents.md)).

The only **possible actions** to execute to achieve the goal are thus moving the parcel from **one position to the next one and waiting for the green light** and **not moving** when there is a **red light**.

![](Verification%2046_image_1.png)

- *Initial states*: 
	white states
- *goal states*: 
	black states
- *Two variables*:
	position (inertial) and color of the traffic light (non-inertial)
- **actions:**
	wa. -> wait
	transp. -> transport


## 3.1 Plans
- How do we represent a plan?
	A plan can be represented by means of a state-action table SA, that is, a set of pairs $(s, a)$, where $s \in S$, $a \in A$, and $a$ is enabled in $s$.
	  
	Special cases:
	 - **Deterministic plans**: for each $s \in S$, there is at most one pair $(s, a) \in SA$. 
	 - **Universal plans**: for each $s \in S$, there is at least one pair $(s, a) \in SA$.

- An alternative representation of plans can be given that distinguishes between the states of the agent/system and the possible contexts.
	
	It makes use of the following constructs:
	 - a function $ACT(q, c)$, that specifies the action to execute when the agent/system is in state $q$ in context $c$
	- a function $CTXT(q, c, q' )$, that associates a new context with the state $q'$ which is reached by executing the action $ACT(q, c)$.

## 3.2 Execution structures
The execution of a state-action table (a plan) in a planning domain can be described in terms of the transitions induced by the state-action table (execution structure). The resulting graph
specifies all the possible executions of the plan.

Formally, let $SA$ be a [[state-action table]] of a planning domain $(P, S, A, R)$. The execution structure induced by $SA$ from the set
of initial states $I$ is a [Kripke structure](Kripke%20structure.md) $K = (Q, T )$, where $Q \subseteq S$ and $T \subseteq S \times S$ are the minimal sets satisfying the following conditions:
-  if $s \in I$ , then $s \in Q$
-  if $s \in Q$ and there exists $(s, a) \in SA$ such that $R(s, a, s')$, then $s' ∈ Q$ and $T (s, s' )$

A state $s \in Q$ is a terminal state of K if there exists no $s' \in Q$ such that $T(s, s')$.

# 4 The [[Execution structure]]

An [Execution structure](Execution%20structure.md) is a [Directed graph](Directed%20Network.md), whose nodes are all the states that can be reached by executing the actions in the [state-action table](state-action%20table.md) and whose edges represent possible action
executions. It is not required to be ==total==, that is, it may include nodes (states) with no outgoing edges (terminal states). Terminal states are states where the execution stops.

Let K = $(Q,T)$ be the execution structure induced by a state-action table $SA$ from $I$ . An execution path of $K$ from $s_0 \in I$ is a (possibly infinite) sequence of states of $Q$ such that, for all
states $s_i$ in the sequence, 
- either $s_i$ is the last state of the sequence (a terminal state of K ) 
- (ii) $T (s_i , s_i+1 )$ (there is an outgoing node)

We say that a state $s'$ is reachable from a state $s$ if there is path from $s$ to $s'$ . We say that $K$ is an [[acyclic execution]] structure if all its execution paths are finite.

![](Verification%2046_image_2.png)

Notice that such a plan does not guarantee to always reach the goal. Basically, it executes the action of **transportation** whenever the color of the traffic light is **green**.


# 5 [The planning problem](The%20planning%20problem.md), a definition

Let $D = (P, S, A, R)$ be a planning domain. A planning problem for $D$ is a triple $(D, I , G )$, where 
- $I \subseteq Q$ is the set of initial states 
- and $G \subseteq S$ is the set of goal states.

Notice that there are two forms of nondeterminism:
-  set of initial states (uncertainty about initial conditions); 
- transition relation (nondeterministic action executions).

The solutions of a planning problem satisfy a reachability requirement: a solution plan is a [state-action table](state-action%20table.md) that, starting at any state in I , allows one to reach a state in $G$.

In fact, the reachability requirement can be met in different ways.

## 5.1 The deterministic case
Let $D = (P, S, A, R)$ be a planning domain, $(D, I , G )$ be a planning problem for $D$, $SA$ be a deterministic [state-action table](state-action%20table.md) for $D$, and $K = (Q, T )$ be the [Execution structure](Execution%20structure.md) induced by $SA$ from $I$ .


>[!Note] Terminal state vs Goal state
>A **terminal state** is a state which we can not leave any more.
>A **Goal state** is a state where we reached our goal.
>A goal state does not need to be a terminal state
>A terminal state does not need to be a goal state
>A state can both be a terminal and a goal state 

We distinguish among weak, strong, and strong cyclic deterministic solutions to the planning problem.

-  **Weak solutions**:
	SA is a weak solution if, for any state in $I$ , some terminal state of $K$ belonging to $G$ can be reached. This is an *existential condition* only one terminal state needs to be reached.

- **Strong solutions**:
	$SA$ is a strong solution if $K$ is [acyclic](acyclic%20execution.md) and all terminal states of K are in G . We always reach the goal) This is a *universal condition* all terminal states need to be reached.

- **Strong cyclic solutions**:
	$SA$ is a strong cyclic solution to the planning problem if from any state in Q some terminal state of K is reachable and all the terminal states of K are in G (they guarantee the achievement of the goal when the execution is [Fair](Fair.md)”).

**Strong cyclic solutions** $\subseteq$ **strong solutions** $\subseteq$ **weak solutions**

### 5.1.1 A note on strong solutions
Strong cyclic solutions capture the idea of “acceptable” trial-and-error strategies: all their partial executions can be extended to obtain a finite execution path whose terminal state is a goal state.

However, they can produce executions that loop forever.

This happens when an infinite sequence of “bad choices” is done, that is, all the infinite execution paths are “**unfair**” because they eventually enter loops where some actions are executed infinitely often in some states where alternative actions leading to the goal were also enabled (and never executed).

## 5.2 The nondeterministic case

Let $SA$ be a nondeterministic [state-action table](state-action%20table.md) $SA$. A **determinization** of $SA$ is any deterministic state-action table $SA' ⊆ SA$ such that $\{s : (s, a) \in SA' \} = \{s : (s, a) \in SA\}$. 

>[!Note] What means **determinization** in practical terms
>We have to choose one of the possible options that the [state-action table](state-action%20table.md) gives us. Then if the path that we choose fullfills the solution condition, we have found one of the deterministic solutions.
>


A **nondeterministic** [state-action table](state-action%20table.md) $SA$ is a weak (resp., strong, strong cyclic) solution to a planning problem if all the determinizations of $SA$ are.

**Strong solutions** to a planning problem are a subset of strong cyclic solutions which are in turn a subset of weak solutions.

**Direct algorithms** for weak, strong, and strong cyclic planning have been proposed in the literature (Weak, strong, and strong cyclic planning via symbolic model checking, by A. Cimatti, M. Pistore, M. Roveri, and P. Traverso, Artificial Intelligence, Volume 147(1–2), July 2003, pages 35-84).

--- 
47 a

---

# 6 Algorithms
We start at the goal and then calculatae attractors...

![](Verification%2046_image_3.png)

The full description can be found in the paper:
Weak, strong, and strong cyclic planning via symbolic model checking, by A. Cimatti, M. Pistore, M. Roveri, and P. Traverso, Artificial Intelligence, Volume 147(1–2), July 2003, pages 35-84).

## 6.1 Representating the [planning domain](The%20planning%20problem.md) symbolically?

### 6.1.1 Domain
The symbolic representation of a planning domain $D = (P, S, A, R)$ is as follows.

First, we associate a **Boolean Variable** with each element of $P$.

The **set of states** $S$ is represented by means of a vector of variables  $\vec{x}$ .

A $state$ $s \in S$ is specified by a formula $\epsilon(s)$  consisting of the conjunction of the variables which are true in $s$ and of the negation of those which are false in $s$.

A set of states $Q \in S$ is thus represented by the formula:
$$\epsilon(Q)=\bigvee_{s\in Q}\epsilon(s)$$

### 6.1.2 Actions 
Actions are represented by means of another set of Boolean variables (action variables).

We can use a distinct action variable for each action in $A$. This allows for the representation of concurrent actions. In case no concurrent actions are allowed, a mutual exclusion constraint must be imposed.

In case concurrent actions are excluded, it is possible to use only $[log |A|]$ action variables $\vec{\alpha}$, where each assignment to the action variables denotes a specific action to be executed (the mutual exclusion constraint is not necessary).

### 6.1.3 Transitions
Transitions are triples **(state, action, state)**. A third vector $\vec{x}'$  of propositional variables, called **next state variables**, is introduced. We require $\vec{x}$  and $\vec{x}'$ to have the same number of variables, and the variables in the same positions to correspond.

We make use of $\epsilon'(.)$ (the obvious adaptation of $\epsilon(.)$) to specify the next state.

A transition is represented by an assignment to $\vec{x},\vec{\alpha}$ and $\vec{\alpha}$ .

Formulas that represent the states of the domain, the transition relation, the initial states, and the goal states by $S(\vec{x} )$, $R(\vec{x} , \vec{\alpha} ~ , \vec{x}' )$, $I (\vec{x} )$, and $G(\vec{x})$, respectively.


### 6.1.4 The plan in symbolic representation

The machinery for the symbolic representation of planning domains can be used to represent and manipulate symbolically the other elements of the planning algorithms, in particular the [state-action table](state-action%20table.md)s (plans).

Let us denote by $SA(\vec{x} , \vec{\alpha})$ the formula corresponding to the [state-action table](state-action%20table.md) $SA$.
- States of the state/action table:
	$StatesOf(SA) = \exists \vec{\alpha}(SA(\alpha{x} , \vec{\alpha} ))$

- Actions of the state/action table associated with a state s:
	$ActionsOf(SA) = \exists \vec{x} (SA(\vec{x} , \vec{\alpha} ))$


### 6.1.5 Planning algorithms
The planning algorithms can be expressed in terms of transformations over propositional formulas.

The basic steps of the algorithms are the following preimage operations that, rather than returning set of states, construct state-action tables.

- Weak Preimage:
	$\exists \vec{x}'(R(\vec{x},\vec{\alpha},\vec{x}') \land Q(\vec{x}'))$
- Strong Preimage:
	$\forall \vec{x}'(R(\vec{x},\vec{\alpha},\vec{x}') \to Q(\vec{x}') \land APPL(\vec{x},\vec{\alpha})$

Where the actions enabled at a given state are expressed as follows:
$APPL(\vec{x},\vec{\alpha})= \exists \vec{x}'(R(\vec{x},\vec{\alpha},\vec{x}'))$

# 7 The action description language $AR$
One of the first action description languages proposed in the literature to model planning problems in nondeterministic domains
is $AR$.

- $A \text{ causes } P \text{ if } Q$: 
	in any state where $Q$ holds, once $A$ has been executed, $P$ holds
-  $A \text{ possibly  changes } F \text{ if } Q$:
	if $A$ is executed in a state where $Q$ holds, the value of $F$ may change
- $\text{always } P$: 
	$P$ holds in all states
- $\text{initially } P$:
	$P$ holds in all initial states 
- $\text{goal } G$ :
	$G$ holds in all final states

![](Verification%2046_image_4.png)

4: We can not execute $wait$ if we are not at the $\text{traffic light}$
5 till 7: At each time we are in exactly one state (traffic light or airport or station)

## 7.1 How can we represent states in $AR$

States in $AR$ are represented by those valuations that satisfy $\text{always }P$.

$$State =\bigwedge_{\text{always } P} P$$
Initial and goal states must satisfy, in addition, $\text{initially }P$ and $\text{goal } G$ , respectively.

$$Init =\bigwedge_{\text{initially } P} P$$
$$Goal =\bigwedge_{\text{Goal } P} P$$

## 7.2 Actions in $AR$

 Actions are associated with a set of variables, called action variables, that are true if and only if the corresponding action is executed.

To model the effects of the execution of an action (the countepart of the $AR$ statement $A \text{ causes } P \text{ if } Q$ ), we need to force the updated values of fluents to define valid states where $P$ holds if $Q$ holds in the current state.

![](Verification%2046_image_5.png)

In addition, we must constrain inertial fluents $F_1 , \dots, F_m$ , with $m \leq n$, to be possibly affected only by the execution of the action or by a condition of the form $A \text{ possibly changes } F \text{ if } Q$.

