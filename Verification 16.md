# 1 Computations of a [[Fair Transition Systems|FTS]]
We have a infinite sequence of states $\sigma = s_0,s_1...,s_n$ where $s_i \in \Sigma$ the set of all states.

$t$ is enabled at position $k$ if it is enabled in state $s_k$

We say $t$ is executed at position $k$ if  $s_{k+1} \in t(s_k)$ i.e the transition function $t$ is actually executed.

==multiple transitions $t$ can be taken at the same position, to the same target==. This is similar in a graph if we have multiple links from one node to another.

## 1.1 [[P-Computation]]

A computation is called [[P-Computation]] of a [[Fair Transition Systems|FTS]] if it satisfies the following conditions:

- [[Rule of Initiality]] $s_0$ satisfies  $\Theta$ and is therefore a initial state
- [[Rule of Consequentiality]] for all $j=1,2,3,...n$ $s_{j+1}$ is a sucessor of $s_j$ for some $t$. i.e. every state has a sucessor.
- [[Justice]]:  all $t \in \mathcal{J}$ need to have [[Justice]].
- [[Compassion]] all $t \in \mathcal{C}$ have [[Compassion]]

[[Justice]] and [[Compassion]] are called <mark style="background: #014E11F2;">Fairness requirements</mark>

One can think of a [[Fair Transition Systems|FTS]] as a graph + Fairness requirements

## 1.2 Properties of Computations
### 1.2.1 [[P-accessible]]
A state is [[P-accessible]] if it occurs in some [[P-Computation]].

Each state that is a $t-sucessor$ of a [[P-accessible]] state is also [[P-accessible]].


### 1.2.2 [[run]]
Is a set of states $\sigma$ that has:
-  [[Rule of Initiality]] i.e. has a initial state
-  [[Rule of Consequentiality]] i.e. every state has a successor.

It does not need [[Justice]] and [[Compassion]] which is necessary for the [[P-Computation]]

Every finite prefix of a [[run]] is a prefix of a ==computation==


# 2 [[Simple Programming Language]]
A [[Simple Programming Language|SPL]] programm is a finite sequence of (maybe) instructions.

The set of [[Simple Programming Language|SPL]] instruction can be partitioned into four 
main classes:

- basic instructions
- schematic instructions
- compound instructions
- grouped composite instructions


## 2.1 Basic instructions
- `skip`
	Is simmilar to the $NOP$. It moves the program counter from before the skip to after the skip.
- `assignment`
	assigns one or multiple values to one or multiple variables:
	$(u_1,..,u_n):=(e_1,....,e_n)$
	
- await
	syntax: `await c`
	`c` is a bool called guard. It waits for `c` to become true. Then the program counter goes on.
	if `c` is false the operations becomes disable
	
- send/receive (synchronous and asynchronous communications)
- send
	syntax $\alpha \leftarrow e$
	- $\alpha$ is a channel (special system variable)
	- e is an expression which type is compatible to $\alpha$
	semantics: e is evaluated and assigned to $\alpha$

- receive
	syntax $α \rightarrow e$
	- $\alpha$ is a channel (special system variable)
	- e is an expression which type is compatible to $\alpha$ 
	semantics: the value of $\alpha$ is assigned to e
	==If the channel does not contain any value the execution of the instruction is delayed.==
	
- request/release (semaphore management)
- request
	syntax: `request r` 
	r is an int
	the instruction is only executed if $r>0$
- release
	syntax: `release r`
	increases the value o `r` by `1`

## 2.2 Schematic instructions
represents sequences of instructions whose details are not of interest.

==We only care if the set of instructions terminates or not.==

It represents a set of instrutions with certain features.

### 2.2.1 noncritial instruction
__syntax__: `noncritical`
It represents a part of the program that we run where we do not use critical resources. It is not necessary that this part of the program terminates as it does not inhibit other parts of programs from running

### 2.2.2 critical instrution
__syntax:__ `critical`
It represents a part of the program that we run where ==we use== critical resources. This demands some coordination between different processes  and ==it must terminate== so that its resources are freed and the other processes can continue.


### 2.2.3 Produce instruction
Syntax: `produce x`
assigns the integer `x` a value different 0. 
It must terminate
### 2.2.4 Consume instruction
Syntax: `consume y`
probably sets y back to 0
It must terminate

## 2.3 Compound instructions
### 2.3.1 __conditional__
syntax: `if c then S_1 else S_2`
like if/else clause
Unlike `await` it is always enabled

### 2.3.2 __Concatination__
syntax: `S_1;S_2;....S_k`
each $S_j$ is one instruction

example: `await c;S` 
would first execute the `await` if c is true then `S` is executed. its like `when c do S`

### 2.3.3 Selection
syntax: `S_1 or S_2 or ... S_n`

It chooses one of the enabled instructions nondeterminsitically. And then the chosen instruction to execute.
If no instruction is enabled, the execution is delayed.

example:
`[when c1 do S_1] or [when c2 do S_2]`

### 2.3.4 While instruction
syntax: `while c do S`

Note: after execution of `S` the program pointer goes back to the position before c. 

Note: If `c` is false when encountering `S` is never executed.

example:
`while True do S`

### 2.3.5 cooperation instruction
it aims to model parallel execution of a given set of instructions
syntax: 
$$l: [l_1:S_1:\hat{l_1}] ||...|| [l_k:S_k: \hat{l_k}];\hat{l}$$
$l$ -> kind of the program counter
- __entry step__: gives the control $l$ over to $l_1$ to $l_k$.
- __exit step:__ When all the executions $S_1$, ...$S_n$ are done and the control is at $\hat{l_1}$,...,$\hat{l_n}$ the control is given back to $\hat{l}$.

### 2.3.6 Block instruction
syntax: `[local declaration; S]`

The variable declaration is only valid between the two brackets i.e. `[ ]`

This is often used in for loops

example: `i:=1;while i<= n do [S;i:=i+1]`


## 2.4 Grouped composite instructions
They are used to make some compound instructions atomic.

### 2.4.1 Composite instructions
What are composite instrutions:
- skip, assignment, await, send, receive are basic composite instructions
- $\text{if} S,S_1,...S_k$ are composite instructions
- while, if-then-else, selection and concatination are composite instructions

A composite instruction is denoted by angular brackets $<S>$

- composite instructions are allowed to only have one ==synchronouse== send/receive instruction for each channel i.e.
	$<S,\alpha \leftarrow 1,S_1>$ ==Allowed==
	$<S,\alpha \leftarrow 1,S_1>$ ==Allowed==

Asynchronouse instructions can at most contain one send receive per variable
	$<\alpha \leftarrow 1,....,\alpha \leftarrow 4>$ ==Forbidden==
	$<\alpha \leftarrow 1,....,\beta \leftarrow 4>$ ==Allowed==

## 2.5 Structure for [[Simple Programming Language|SPL]] programs

![[Structure of a SPL program.png]]

## 2.6 Declaration

syntax:
`mode var,..varn: type where phi`

mode can have the following values:
- `in` (it specifies a input variable)
	are read only, used to input values into the program
-  `local` (the variable is local)
- `out` (it specifies a output variable)

phi can be used to constraint the initial values of a variable
- `local/out` can take only the form of `y=e` where e is a `in` variable
- no restriction on the form of `phi` can be anything, could be used to define the set of admissible values.

this restrictions are also called: ==data precondition==

## 2.7 Channel declaration

- sinchronous
	$\text{mode }a_1,...,a_n:\text{ channel of type}$
- asinchronous
	$\text{mode } a_1,...,a_n: \text{ channel }[1...] \text{of type where } \phi$
	$[1,..]$ denotes a buffer of unbounded capacity, $\phi$ speciies conditions on the initial state of the content of the buffer (if $\phi$  is empty the buffer is assumed to be empty)


## 2.8 sinchronous vs asinchronous
in sincronous communication the send and receive has to be done at the same time (no memory).

In asinchronous communication the sender can start sending the message, the receiver can receive the message after some time.


## 2.9 Example: Calculate the greates common divisor

![[Verification 17_image_2.png]]


$y_1<>y_2$ $\equiv$ $y_1 \neq y_2$













