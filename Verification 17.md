 In this class we will translate a [[Simple Programming Language|SPL]] programm to [[Fair Transition Systems|FTS]] [[Deterministic Finite State Automata|Automata]].

# 1 Labels
Used in two ways:
- identifying instructions
- localize where the control pointer is 

> [!note]
> multiple labels can define the same place of the control pointer

We create a [[Equivalence Relation]] that allows us to identify labels that are associated with the same location.

$$l_y \sim _L l_x$$

This means that $l_y$ an $l_x$ are associated with the same program counter position.

![[equivalent control pointer positions.png]]

As a description from above
1. case $l \sim l_1$ and only to $l_1$ -> this is a concatination
2. case $l \sim l_1 \sim l_2 \sim ....\sim l_k$ this is a conditional
3. $l \sim l_1$ and only to $l_1$ -> this is a assignment -> local declaration does not 

How does this look for our example of the GCD:
![[GCD in SPL.png]]

![[control locations for the GCD.png]]

How does the $[l_2]$ class work out?
1. we have $l_2$ is infront of a conditonal (case 2)
2. then we have a concatination (case 1), $l_2$ is equal to the first command of the concatination

## 1.1 [[Post-location]]s
Is an instruction executed, a new location is reached. This location is called [[Post-location]].

Example:
![[post location instruction.png]]

The [[Post-location]] of this instruction $S$ is the location of the last command that is executed i.e. $S_k$.

i.e. $post(S) = post(s_k) = l_k$
for all other commands i.e. $l_i...l_{k-1}$ the [[Post-location]] is simply $l_{i+1}$

Other examples:

![[other post location examples.png]]

How does it look with our GCD example?

![[Post location GCD.png]]

## 1.2 The [[Ancestor relation]]

If $S'$ is a sub instruction of S, S is called the __ancestor__ of $S'$

![[The ancestor relation.png]]

Example for [[Ancestor relation|LCA]]:

![[Largest common ancestor example.png]]

==What does this mean==: Looking at the [[Ancestor relation|LCA]] we can see if the instructions can be executed in parallel or need to be executed one after another.

When can we execute two instructions in parallel?
> [!note] parallel instructions
> If $s_i$ and $s_j$ have a cooperation instruction ($||$) S, where $S_i \neq S_j$ and $S_j \neq S$ and $S_i \neq S$ then they are __parallel instructions__ and we can execute them in parallel. Otherwise we call them __instructions in conflict__

Example:
![[Parallel instructions example.png]]

## 1.3 Semantics of [[Simple Programming Language|SPL]] programms


The [[semantics]] of an [[Simple Programming Language|SPL]] program are simmilar to an [[Fair Transition Systems|FTS]]:
$$\{V,\Theta,\mathcal{T},\mathcal{J},\mathcal{C}\}$$
The computation of an [[Simple Programming Language|SPL]] program are the computations of a corresponding [[Fair Transition Systems|FTS]]

## 1.4 $V$ the variables
$V$ collects the set $Y=\{y_1,...,y_n\}$ of program variables and a __control variable__ $\pi$.

The __control variable__ saves the location of the control during execution.

$$V = \{y_1,y_2....,y_n\} \cup \{\pi\}$$

### 1.4.1 Example at the GCD
$V=\{\pi,a,b,y_1,y_2,g\}$

The domain of $\pi$ is the powerset of $\{[I_1],[I_2],[I_4],[I_6],[I_7]...,[I_8]\}$

The value of $\pi$ is a subset of $\{[I_1],[I_2],[I_4],[I_6],[I_7]...,[I_8]\}$. It might be just one of them or all of them.

==Special case==
<mark style="background: #FFB8EBA6;">Asynchronous channel</mark>: For every asynchronous channel one gets one variable for storing the variable written to the channel.
<mark style="background: #FFB8EBA6;">Synchronous channel</mark>: There is no need of an additonal variable as the value is written and read at the same time.

 Notation:
 $@_l$ is a shorthand for $[l] \in \pi$
 $@_l'$ is a shorthand for $[l] \in \pi'$ so the location in the next state

## 1.5 The initial condition $\Theta$  
The intial condition consist of the conditions for the input variables (in this case $a,b$) and the initial variables (in this case $y_1,y_2$) and a starting position for $\pi$

The conditions are:
- $a>0$
- $b>0$
- $y_1=a$
- $y_2=b$
- $\pi={[l_1]}$

![[Initial condition example.png]]
  

## 1.6 The set of transistions $\mathcal{T}$ 
1. The set of transitions has also the ideling transition $\mathcal{T_I}$ which does not move the change any of the variables.
2. All transitions are [[self-disabling]] meaning that at least the control variable is changed.

Abbreviations:
![[Abbreviations transitions.png]]

==$pres$ stands for preserve==

### 1.6.1 Lets start translating basic instructions:
#### 1.6.1.1 $l: skip(\hat{l})$
	$\rho_l:move(l,\hat{l}) \land pres(Y)$
	explenation: it moves the control location from $l$ to $l'$ but preserves all other variables
#### 1.6.1.2 assignment $l:  \bar{u}:=\bar{e}; \hat{l}$
	 $\rho_l: move(l,\hat{l}) \land \bar{u'}= \bar{e} \land pres(y-{\hat{u}})$
	 explenation: it moves the control location, assignes $e$ to the value of $u$. All variables are preserved, except $u$.
#### 1.6.1.3 `await` $c;\hat{l'}$ :
- $\rho_l: move(l,\hat{l}) \land c  \land pres(Y)$
explenation: when c is true the entire statement gets true and executed. if c is not true the statement cant be true.
#### 1.6.1.4 Asynchronous send: $I: \alpha \leftarrow e; \hat{l}:$
$\rho_l: move(l,\hat{l}) \land \alpha' = \alpha \cdot e \land pres(Y-\{\alpha\})$ 	 
 - $\cdot$ is the concationation operation

#### 1.6.1.5 Asynchronous receive: $I: \alpha \leftarrow e; \hat{l}:$	$\rho_l: move(l,\hat{l}) \land |\alpha|>0  \land \alpha = \alpha' \cdot u' \land pres(Y-\{u,\alpha\})$	 
The transition is only enabled if the channel is not empty	

$\alpha =u' \cdot \alpha'$ is a fancy way of saying we remove an element from $\alpha$. It means the old $\alpha$ value is the new $\alpha$ value concatenated with $u'$ meaning that  $\alpha'$ is $u'$ less than the original $\alpha$.

#### 1.6.1.6 Synchronous send/receive:

![[SPL to TLS synchronous request and release.png]]

  explenation: we move the control in the two processes from l to $l'$ and from $m$ to $m'$ simultaneously. The control needs to be at $l$ and $m$ simultaneously otherwise the command is not enabled .
  We move the value from the variable $e$ to $u$.
#### 1.6.1.7 Request
![[Reqest SPL to TLS.png]]

#### 1.6.1.8 Release
![[Receive SPL to TLS.png]]

#### 1.6.1.9 $I: noncritial; \hat{I}$
- $\rho_l:move(l,\hat{l}) \land pres(Y)$
#### 1.6.1.10 $I: critial; \hat{I}$
- $\rho_l:move(l,\hat{l}) \land pres(Y)$

critical and noncrital look the same but they have different termination conditons.
$critical$ has [[Justice]]
$noncritical$ does not need [[Justice]] nor [[Compassion]]

#### 1.6.1.11 Produce
![[SPL to TLS produce.png]]

#### 1.6.1.12 Consume
![[SPL to PLS consume.png]]

  
### 1.6.2 lets translate Compound instructions

#### 1.6.2.1 If then else
![[SPL to TLS if else.png]]

It is implemented by having two subformulas $\rho_T$ and $\rho F$ where only one of the two can be true as one contains $\neg c$ and one $c$

#### 1.6.2.2 While

![[SPL to TLS While.png]]

In the cooperation instruction we model first the entry step $\rho_l^E$ and then the exit step $\rho_l^X$.
We move the control to the sub-instruction $l_i$

