We continue with the proof of [[Theorem 6|Myhill-Nerode Theorem]] which was started in [[Verification 12]].

### 0.1.1 Proof 3 -> 1
We assume $\approx_L$ has [[finite index]]
==lets recall:==
  $$u \approx_L v \quad \iff  \quad \forall t \in A^\star \hspace{0.5em} ( u \cdot t \in L \iff v \cdot t \in L)$$

==Goal:==
Contruct a [[Deterministic Finite State Automata|DFA]] $\mathcal{A}$ that recognizes $L$ i.e. $\mathcal{L}(\mathcal{A})=L$

How do we construct such a [[Deterministic Finite State Automata|Automaton]]?

$$\mathcal{A}=(A,Q,\delta,q_0,F)$$

- $Q=\{[u]_{\approx_L} | u \in A^\star\}$
> What does this mean: It means that we create a state for every equivalence class that exists when using the equivalence relation $\approx_L$

- $q_0=[\epsilon]_{\approx_L}$
> We choose the initial state to be the equivalence class of the empty word. i.e $\forall x  \in A^\star \quad | \quad  x \approx_L \epsilon$

- $F=\{[u]_{\approx_L} | u \in L\}$
> We create final states for all equivalence classes which contain at least one word that is part of the language $L$

- $\delta=Q \times A \rightarrow Q$
$\delta([u]_{\approx_L},a):=[u \cdot a]_{\approx_L}$

==But we have a problem!==
We agreed that $[u]_{\approx_L}$ is a state $q$ and $[u \cdot a]_{\approx_L}$ is a state $q'$. When we have two words $u$ and $v$ belonging to $q$ who makes sure that if we [[Concatenation|concatenate]] $t$ (i.e. $u \cdot t, v \cdot t$) that we are come out in the same equivalence class $q'$ and not two different ones like $q'$ and $q''$?

In general: for arbitrary [[Equivalence problem]] we could have a case: $u = v$ but $u \cdot t \not= v \cdot t$

But we have a special case: We have a right invariant equivalence as of the definition:
 $$u \approx_L v \quad \iff  \quad \forall t \in A^\star \hspace{0.5em} ( u \cdot t \in L \iff v \cdot t \in L)$$
Therefore when we use our equivalence $\approx_L$
$$u\cdot t \quad \overset{!}{\approx_L} \quad v  \cdot t$$

Previously we have just assumed that $\approx_L$ is right invariant by definition but we also have to prove it this is the next step

#### 0.1.1.1 Prooving that $\approx_L$ is right invariant
To prove that $\delta$ is well defined we need to check that $\approx_L$ is [[right invariant]].

Our goal is to proove that:
$\forall t':(u \approx_L v \implies u \cdot t' \approx_L v \cdot t')$

So what is the definition of $\approx_L$ it means that $\forall t: u \cdot t \approx_L v \cdot t$ and now we show that $u \cdot t \cdot t' \approx_L v \cdot t \cdot t'$ holds also true i.e. $\approx_L$ is [[right invariant]].

==This is a little bit obviouse== but needs to be shown.

Now the last step is to show that $\mathcal{A}$ recognizes the language $L$

#### 0.1.1.2 Accepts $[u]_{\approx_L}$ the language $L$?

==Note the invariant:==  $\forall w \in \mathcal{A}^\star$ 
If we leave from the initial state $q_0$ we are in equivalence class $[\epsilon]_{\approx_L}$ . When we input $w$ we return in the state $q_w$ which has the equivalence class $[w]_{\approx_L}$.  A schematic can be seen in the diagram below:
$\mathcal{A}:$
 ```mermaid
graph LR
start --> q0
q0(("q0=[epsilon]"))--w-->qw(("qw=[w]"))
qw--a-->qwa(("qwa=[wa]=[w]"))
```

We proof this by induction by the length of $w$ i.e. $|w|$:

if $w \in \mathcal{L}(A) \iff q_w = \delta(q_0,w) \in F$.  This means that If $w$ is part of the accepted words of $A$ then the transition function $\delta$ with the two arguments (which result is the state $q_w$) needs to be an element of the final states $F$.

And when is $q_w$ part of the final states $F$? If it is in the [[Equivalence problem|equivalence class]] $[w]_{\approx_L}$  and this can only be the case if $w$ is part of the language and this is what we needed to show.

$\square$

With this the [[Theorem 6|Myhill-Nerode Theorem]] is proven!

# 1 [[Learning Automata]] ... and generalisations

When we talk of learning we normally mean supervised learning. The architecture is fixed and we only optimize the weights of the nodes so that in the end the [[Neural network]] can then do something for you.

But this time we work with [[Deterministic Finite State Automata|Automata]] because it has other applications:

What are the differences:
The data: for [[Neural network]]s the input is very often a fixed sized tuple of Real numbers. With [[Deterministic Finite State Automata|Automata]] the size is not fixed, the data can even be infinite.


|                      | [[Neural network]]                                                  | [[Deterministic Finite State Automata\|Automata]]                                      |
| -------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Data                 | simple data: $\bar{X}\in \mathbb{R}^k$                              | complex data e.g. : $w \in \Sigma^\star$                                               |
| what can be learned? | complex functions: $\mathbb{R^x} \rightarrow {0,1}$, detecting dogs | simple functions: $f: \Sigma^\star \rightarrow \{0,1\}$, representing regular languges |
| architecture         | architecture is fixed                                               | states+transition are learned                                                          |



## 1.1 Active learning vs Passive learning

The teacher only provides labels and data. But it does not interact with the neural network.
![[Verification 13_image_1.png|300]]

There is a back and forth. The learner asks the teacher and the teacher then responds.

An example: The learner creates a image of a dog. The teacher than says if this is a dog. If not the learner adapts the creation of the image.

Sometimes the active scenario is not ==practial==.
Tends to be more efficient.

![[Verification 13_image_2.png|300]]


## 1.2 bit of history

- __1956__ Moore introduced Active learning: Application we know only the output of the machine. We want to figure out how the input looks like.
- __1986__ Angluin an algorithm how learn an automaton based on queries.
- __1993__ PAC learning find a statistical approximation of a automaton based on queries
- __1995__ learn [[omega language]]
- __1996__ learn word transformations -> automaton that has a word as input and a word as output
- __2015__ Guy from amazon proposes spectral techniques for learning

---
pause

---

# 2 Learning as a game
==Step 1==
The ==teacher== has a secret regular language $L_0$, for instace represented by a [[Deterministic Finite State Automata|DFA]] $A_0$.
The learner initialy only knows the undelying alphabet $\Sigma$

Note: Why [DFA](Deterministic%20Finite%20State%20Automata.md)? Comparing of languages only takes [[P-Time]]

==Step 2==
__Learner__ can choose between two queries while estimating its [[Deterministic Finite State Automata|DFA]] $A$, $A_0$ is the [[Deterministic Finite State Automata|DFA]] the teacher has that describes the language $L_0$:
1. either a __membership query__ "is $w$ in $L_0$"
2. or a __equivalence query__ "is $L(A) = L_0$" or in other words are $A_0$ and $A$ [[Equivalence problem|equivalent]]

This is a cooperative game: The teacher is not the opponent of the learner.

==step 3==
The teacher answers accordingly
1. yes if $w \in L_0$ no if otherwise
2. Yes if $L(A) = L_0$ i.e. the __Learner__ wins and the game ends. Otherwise the teacher will return the shortes possible counterexample: He choses a word $w$ so that $w \in (L_0-L(A)) \cup (L(A)-L_0)$ this is the [[symmetric difference]] of the Languages. This are all the words that either do belong to $L_0$ but not to $L(A)$ i.e. ($(L_0-L(A))$) or they belong to $L(A)$ but not to $L_0$ i.e.  ($L(A)-L_0$).

The fact that the teacher chooses the shortest counterexample has an influence on the complexity of the problem.

==Observation:==
A membership querry is not enough for the learner to win. This is in particular about [[Deterministic Finite State Automata|DFA]]s that have an infinite amount of words. Therfore we outlaw this. The learner can only win by a __equivalence query__.

==Other observation==
__Can we win only using  equivalence queries__?
We can always win by asking only __equivalence queries__ in finitely many steps!!
There are countably many [[Deterministic Finite State Automata|Automata]] therefore we can just go through all of them at some point finding our desired [[Regular Languages|Regular language]].

How fast can we win?
How many queries do we need to do  till we win only using __equivalenece queries__?
The number of queries is exponential to the number of states of the target (secret) [[Deterministic Finite State Automata|Automata]]. If we want to find a [[Deterministic Finite State Automata|Automata]] with 10 states we have to do before the [[Deterministic Finite State Automata|Automata]] with 1 state, 2 states... till we are at 10 states.

So what do __membership queries do?__.
==When using __equivalence queries__ and __membership queries__ one can find the automaton in [[P-Time|polynomial time]].==

> [!note] [[Theorem 7]]
> The learner has always a strategy in a number of rounds in the game that is [[P-Time|polynomial time]] in relation to the number of states of $A_0$

## 2.1 The [[Minimally adequat teacher]] and [[Black-box learning]]

### 2.1.1 [[Minimally adequat teacher|MAT]]
The [[Minimally adequat teacher]] is a perfect teacher that knows the language. Why bother playing the game then? Why should he not just hand over the [[Deterministic Finite State Automata|Automata]] to the learner?

### 2.1.2 [[Black-box learning]]
Well this is true and in practice the [[Minimally adequat teacher]] seldomly is present. We do not have any info on how the  [[Deterministic Finite State Automata|Automaton]] actually looks like. 

We have often a Black box though. Like a machine where we can check if the word send during a __membership query__ is present. For instance we can try the input on the coffemachine where we want to estimate the internal machine.

Then over time we can approximate the [[Deterministic Finite State Automata|Automaton]] by checking again and again the accepted words of the proposed machine of the learner. If the [[Deterministic Finite State Automata|Automaton]] accepts all the words then we can say: Well it looks good. This might be the machine.

In practice this methods are used in ==protocoll state fuzzing== 

---
==from here only lose notes==
---

## 2.2 Applications of the [[Theorem 6|Myhill-Nerode Theorem]] during 
If there is a regular language you can create it by a union of equivalence classes. Each puzzle is one equivalence class. Each [[Equivalence problem|equivalence class]] contains words. 

![[Verification 13_image_3.png|600]]

![[Verification 13_image_4.png|600]]


We will introduce a new equivalence: We do not test the [[Theorem 6|Myhill-Nerode equivalence]] for all words but only for a set of words $T$. With this we might not get the entire truth but we learn more and more about the Language $L_0$.

![[Verification 13_image_5.png]]

Of course as $T$ is a subset of $\Sigma^\star$ i.e. the relation relativizes the entire [[Theorem 6|Myhill-Nerode equivalence]].

If $T$ is empty we define the most broad equivalence because we do not need to check for any words of $T$ and it always returns true i.e. all words are equivalent and we only have one [[Equivalence problem|equivalence class]].

If we define $T$ as the empty word i.e. $\{\epsilon\}$ it results that two words are only equivalent if they are the same with a traditional equivalence i.e. $u=v$. Because we need to check the two words without adding a symbol.

What does this mean. That we have a control knob how accurate we want to estimate the Language $L_0$.
![[Verification 13_image_6.png]]
If we leave $T$ empty we have almost no info. If we choose T to be the empty word we need to test a lot. So between this two extremes we can define our T to fit to our needs.

Myhill rode is a very fine equivalence. The blue and grey puzzle pieces.
The relativeized equivalences are more coarse. The red borders over the puzzle pieces in the image below.
![[Verification 13_image_7.png|600]]



==Definitions==
A learner constructs automata from pairs $(S,T)$. $S \subseteq \Sigma^\star$ and [[T-Minimal]] and [[T-complete]]


[[T-Minimal]]
A set $S$ is minimal that whenever I choose two elements $s$ and $s'$ of $S$  they are never in the same equivalence class. You do not need an element for every class that exists i.e.

![[Verification 13_image_8.png|300 ]]

[[T-complete]]
[[T-complete]] means that for every word $a$ that we concatenate to the right of a word $s$ of $S$. There exists at least one element $s'$ out of $S$ that is equivalent to $sa$ in the T-equivalence $\approx_{L_{0}T}$.


![[Verification 13_image_9.png|700]]


I the end we will define the transitions as the arrows and the red dots as the states resulting in a learned automaton that accepts the language $L_0$.

Now the learner can add more states by increasing T. And reduce the states by reducing the number of elements in T.