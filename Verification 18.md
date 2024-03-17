# 1 The transitions
## 1.1 The Grouped composite instructions $<S>$

We want to make instruction that are not [atomic](atomic.md), execute in a single step, i.e. make them atomic. We need to figure out what the influence of all the instructions on the variables are but not the control variable i.e. $Y$. Kind of like the return value of a function of instructions 

To more easily refer to this change of variables of $Y$ we define the [[relation of data transformations]] $\delta[S]$ which are all the changes of the variables of $Y$ not including $\pi$.

In the easiest case we only remove the $move(l,\hat{l})$. (`skip`,`await`,`assignment`, `asynchronous send and receive`)

In the more complex cases it is defined as follows:

- when
 $\delta[\text{when }c \text{ do } S]: c \land \delta[S]$
 ==note: when is only enabled if c is true==
- conditional:
$\delta[\text{if  c then }S_1 \text{ else } S_2]: (c \land \delta[S_1]) \lor (\neg c \land \delta[S_2])$ 
special case:  
$\delta[\text{if  c then }S_1 ]: (c \land \delta[S_1]) \lor (\neg c \land Pres(Y))$ 
==note: if is always enabled==

- selection and concatenation
![[Verification 18_image_1.png]]

An example:
![[Verification 18_image_2.png]]


## 1.2 The grouped instructions syntax

- $l: <S>;\hat{l}:$
- $\rho_l: \delta[S] \land move(l,\hat{l})$
It differs from $l: S;\hat{l}:$ in that with only $S$ one would need to define every individual step of $S$. This is not atomic.

### 1.2.1 But how does it work with synchronous communications?
![[Verification 18_image_3.png]]

We calculate the delta by:
- first executing $T_1$
- then $T_2$
- Then we do the assignment $u:=e$
- Then $S_1$
- Then $S_2$
## 1.3 The fairness conditions [[Justice]] $\mathcal{J}$ and [[Compassion]] $\mathcal{C}$

$\mathcal{J}$ includes all transitions except with the idling transition and all `noncrital` instructions.

$\mathcal{C}$ includes all transitions associated with:
- `send` and `receive`
- grouped instructions including communication instructions
- the `request` instruction for the managment of semaphores

# 2 [[Reactive Program]]s
An example of a [[Reactive Program]]:
![[Verification 18_image_4.png]]

__P2__ never terminates
Since we require [[Justice]] we will move from $m0$ to $m1$
Also $m1$ needs to be executed as we require [[Justice]]

This is not a addmissible [[P-Computation]] as only $l_{0a}$ satisfies [[Justice]] as it is constantly enabled. On the contrary $l_{0b}$ is not constantly enabled and never executed -> no [[Justice]]

Another un-[[Justice|just]] program:
![[Verification 18_image_5.png]]

It can also not guarantee termination:
We can not guarantee that the condition is true from a certain point on.

The point is that the controller can never be sure that $m1$ or $m2$ are not disenabled while executing therefore he might just not execute any.

Another case:
![[Verification 18_image_6.png]]

One can not get stuck at $l_0$ because of the $else$ statement. Only [[Justice]] is necessary to make sure that $P1$ is demanded.

![[Verification 18_image_7.png]]


Now the classical [[Mutual exclusion Problem]]:

![[Verification 18_image_8.png]]

What is [[Mutual exclusion Problem|Mutual exclusion]]?
We want to make sure that only one of the programs can access the shared resource.

[[Accessibility property]]:
If a program tries to access a resource, sometimes in the future, it will  be able to access the resource. It will never be the case that it can never access the resource.





How do we show [[Mutual exclusion Problem|mutual exclusion]]?
Can show only using [[Justice]]

![[Verification 18_image_9.png]]

How do we prove [[Accessibility property|accessibility]]
Here we need both [[Justice]] and [[Compassion]] 
![[Verification 18_image_10.png]]

![[Verification 18_image_11.png]]


