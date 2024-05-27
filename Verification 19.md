# 1 [[Safety property]]
During the state of computation, it is never the case that two processes access a critical resource at the same time.


## 1.1 Using a grouped instruction to try make a code safe

![[Verification 19_image_1.png]]

The command within the $<>$ is the grouped instruction.

1. Issue is the safety property still valid in this code peace
	It is important that the $when$ and the $y=y+1$ is grouped. If it is not executed at the same time when $P_1$ starts the critical block, before decreasing $y$ i.e. $y=y+1$, $P_2$ starts with its critical block as well... safety is not longer guaranteed. By using a Atomic instruction $when$ and $y=y+1$ is happening at the same time.
2. Issue [[Accessibility property]]  
	[[Accessibility property]] is ==not guaranteed== because when both programs are at $l_2$ and $m_2$. $when$ is not gets disabled for the process that has not accessed the critical resource. As it is not always enabled anymore, the [[Justice]] argument does not hold. We would need [[Compassion]] to have influence on and off switching instructions. As we do only have [[Justice]] it means that we can not guarantee [[Accessibility property|Accessiblity]]

>[!Note:]
> This program has the property [[Communal Accessibility]]

Is a weaker form of [[Accessibility property|Accessibility]].

> [!note] Definition
> Whenever a group of agents tries to access a critical resource it will be accessed by one of them in the future. 

## 1.2 Producer-consumer with a bounded buffer

==Goal:==
We want to make that we can not put more than $n$ elements into the buffer.


![[Verification 19_image_2.png]]

$send$ is empty, $ack$ contains $n$ ones.
$send$ and $ack$ are [[Asynchronous messaging|asynchronous channels]].

## 1.3 Fair-Merge
The goal of this program is that if we have two producers, providing their goods, none of the goods are prefered by the consumer. I.e. No one of the two producers is discriminated against.
$a_1,a_2$ -> synchronous channels
$b$ -> asynchronous channel

What is the difference between $P_1$ and $P_2$?
- $P_1$ puts $2 \cdot x_1 +1$ in his channel
- $P_2$ puts $2 \cdot x_1$ in his channel
Now all the numbers of $P_1$ are even, and of $P_2$ are uneven. We can distinguish from which producer the good comes and can still reconstruct the message 

![[Verification 19_image_3.png]]

Due to [[Compassion]] it is not possible that $m1b$ or $m1a$ are never executed as the instructions are switched on and of every iteration of the merger.

---
brake

---

# 2 Finite state automata on infinite words
We want to go from:
[[Finite State Automata]] $\rightarrow$  [[Buechi automata]]

[[Buechi automata]] work on infinite words.

Infinite words over a finite alphabet $A$ we might also call them as [[omega-words]] are a infinite sequence of symbols from the alphabet $A$.

---

$A^*$ is the set of all finite words over the alphabet $A$.
$w,u,v$ are finite words of the alphabet of finite words $A^*$.
$w,u,v \in A^*$

---

$A^\infty$  = the set of all infinite [[omega-words]] and all finite words i.e. $A^w \cup A^*$ 

---

$A^w$= is the set of all infinite [[omega-words]] over alphabet $A$

$\alpha,\beta,\gamma \in A^w$

to denote individual symbols of $\alpha$ we call it by $\alpha(1)$ or $\alpha(2)$, which is the first and second symbol respectively.

To address a consecutive set of symbols i.e. from position 4 to position 8 we write: $\alpha(4,8)$

To write all symbols from a certain position we write: $\alpha(4,w)$ which is all symbols from position 4 till $\infty$ .

$\exists^w n$ this means there exist ==infinitely many== $n$ for which something holds

$\exists^{<w} n$ this means there exist ==finitely many== $n$ for which something holds

[[w-closure]] $w$
Now we want to create infinite words from repetitions of infinite words:
We write this in the following way:
$w^w=\{\alpha \in A^w: \alpha=w_0,w_1,w_2\}$
where: $w_n \in w$

$\alpha$ are the words that can be created by repeating the infinite words of $\omega$ a couple of times. Some words might be repeated multiple times.

[[Vectorial closure]] of $w$
This are all words $\alpha$ that have infinitely many prefixes in the word $w$
$\overrightarrow{w}=\{\alpha \in A^w: \exists^w n \quad \alpha(0,n) \in w \}$    


An image:

![[Verification 19_image_4.jpeg]]


For all $\alpha \in A^w$, we define:
$In(\alpha) = \{a \in A:\exists^w n \quad \alpha(n)=a\}$
This means that for every symbol $a$ of the alphabet $A$ there are infinite occurences of  it in the infinite word $\alpha$.
This is never empty: Because if we have a infite word created from an finite alphabet some symbol must occur infintely many times.

> [!note] note
> The standard task in finite word automata: is a word accepted by the automaton, i.e. is in the alphabet can not be done in infinite word automata. We have no chance to check if a word might not occur at the later time...


---



# 3 [[Buechi automata]]
Are a special case of infinte word, [[Non deterministic]] [[Deterministic Finite State Automata|Automata]].

$$\mathcal{A}=\{Q,A,\Delta, q_0,F\}$$
All states are similarly defined as in [[Non Deterministic Finite State Atomata|NFA]]

$\Delta \subseteq Q \times A \times Q$ 
$Q$ is the set of states. This means that $\Delta$ is the set of states reachable from a state when reading in a word from $A$. Why are this mutliple states? Because it is [Determinism](Determinism.md)

## 3.1 [[P-Computation]]

A [[P-Computation]] of $\mathcal{A}$ on an [[omega-words|w-word]] $\alpha$ is an [[omega-words|w-word]] $\sigma$ over a set of states $Q$ such that:
1. it needs to start from an initial state
	$\sigma(0)=q_0$
2. [[Rule of Consequentiality]]
	for all $i \geq 0$ $(\delta(i),\alpha(i),\delta(i+1) \in \Delta$ 
	i.e. there always needs to be a next state $\delta$ 
1. termination computation
2. We say that a [[P-Computation]] $\sigma$ on $\alpha$ is successful if $In(\sigma) \cap F \neq \emptyset$. 
	This means that at least one state of  $\sigma$ is repeated infinitely many times and this state describe a state that is also a final state i.e. is member of $F$.

The [[Deterministic Finite State Automata|Automaton]] $\mathcal{A}$ accepts a word $\alpha$ if there exists at least one successful computation ([non-deterministic](Determinism.md)) of the Automaton on $\alpha$.

The language accepted by the [[Deterministic Finite State Automata|Automaton]] $\mathcal{A}$ is the set of all [[omega-words|w-word]]s  accepted by the [[Deterministic Finite State Automata|Automaton]].

A [[omega language|w-language]] $L \subseteq A^w$ is [[w-regular]] if it is a accepted by a [[Buechi automata]], that is there exists a [[Buechi automata]] $\mathcal{A}$ so that $L(A)=A$. 








