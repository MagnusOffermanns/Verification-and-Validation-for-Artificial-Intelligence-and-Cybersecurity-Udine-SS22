# 1 [Model-checking](Model-checking.md) in [CTL](Branching%20time%20temporal%20logic.md)
Given the [temporal structure](Kripke%20structure.md) $M$ and the [CTL](Branching%20time%20temporal%20logic.md) formula $\phi$  do the following for the subfolder $\psi$ of $\phi$ (according to an increasing order of their complexities)

compute $[\psi]=\{r \in S|M,r \models \psi\}$

Finally check if $s \in \phi$


==Remark:== If  $M$ is finite, this can be done effectigely by fixed-point computations.

==Complexity:== Polynomial
- linear in $|M|(|S|+|R|)$
	- $S$ -> Nodes
	- $R$ -> Edges
- linear to the size of the formula i.e. $|\phi|$ 

>[Note] Difference to [LTL](temporal%20logic.md) [Model-checking](Model-checking.md)
>In [LTL](temporal%20logic.md) model checking we need to build a [Tableaux](Tableaux.md). because we need to build a [Tableaux](Tableaux.md) we might get an exponential blowup in relation to the size of the formula.
>
>In [CTL](Branching%20time%20temporal%20logic.md) [Model-checking](Model-checking.md) we do not need to build a [Tableaux](Tableaux.md) therefore the computational comlexity is only polynomial.



---

36 b

---


## 1.1 Example microwave

==Informal definition of a microwave oven:==

To cook food in the oven, open the door, put the food inside, and close the door. Do not put metal containers in the oven. 
Press the start button. The oven will warmup for 30 seconds, and then it will start cooking. When the cooking is done, the oven will stop. The oven will stop also whenever the door is opened during cooking. If the oven is started while the door is open, an error will occur, and the oven will not heat. In such a case, the reset button may be used.

This is the behavior as a model, we can call it program.

![](Verification%2036_image_1.png)
We have four proposition letters
- $start$
- $close$
- $heat$
- $Error$

We also describe faulty behavior. This are normal states, but we only label them as "faulty behavior".

One note: If one is in a error state, one can open and close the door without that the microwave starting. The only way to recover from the error is closing the door and pressing the reset button.

### 1.1.1 Specification
1. If the oven heats, then the door is closed:
	$A(G(Heat \implies Close))$
2. Whenever the start button is pushed, eventually the oven will heat
	$A(G(Start \implies A(F(Heat))))$
3. Whenever the oven is correctly started, eventually the oven will heat
	$A(G((Start \land \neg Error) \implies A(F(Heat))))$
4. Whenever an error occurs, it will still be possible to cook
	$A(G(Error \implies E(F(Heat))))$

Specification 1 is true, as in the only two states where $Heat$, $Close$ is also true.

![](Verification%2036_image_2.png)

The specification 2 is $false$, due to the error state, one can find a circle where the oven will not heat...

![](Verification%2036_image_3.png)

The $3^{rd}$ specification is also true as we only have one path where this might be true:

![](Verification%2036_image_4.png)

The $4^{th}$ specification is also true, as we can recover from a error by pressing the reset, then we can heat again. The below path is one path to go heating again.

![](Verification%2036_image_5.png)



This is the kind of checking we want to do: We have a Model $M$ and a formula $\phi$. Does the formula hold on the entire Model?

## 1.2 Algorithm

We elaborate subformulas in increasing length order (like in the modal case). I.e we start from small formulas and go on checking bigger and bigger ones.

Cases $EX$ and $AX$ are resolved by visiting the ==successors== of the current state. However, cases $EU$ and $AU$ impose us to visit, in the worst-case, all the nodes reachable by a path from the current state. We will take advantage of the following recursive definitions:

$$EU(\alpha,\beta)=\beta \lor (\alpha \land EXEU(\alpha,\beta))$$
$$AU(\alpha,\beta)=\beta \lor (\alpha \land AXAU(\alpha,\beta))$$

Basically we check if in the next step $\beta$ is already true, making the $U$ true or $\alpha$ is true and we go to the next state ($EX$) where we check the modality again (either $EU$ or $AU$).

I proceed till i find $\beta$, till then $\alpha$ must be $true$.

>[!Note] syntax note
>$AU(\alpha,\beta) \equiv A((\alpha)U(\beta))$

The input is a [temporal structure](Kripke%20structure.md) $\mathbb{M}=<M,R,V>$ and a [CTL](Branching%20time%20temporal%20logic.md) formula $\alpha$
$M$=Set of states
$R$=Transition functions
$V$= Labeling function sometimes also referred to as $L$

![](Verification%2036_image_6.png)
![](Verification%2036_image_7.png)

![](Verification%2036_image_8.png)

![](Verification%2036_image_9.png)

### 1.2.1 Computational complexity
Let $n = |M|$ be the number of nodes, $m = |R|$ be the number of edges, and $k$ be the length of $α$ the [LTL](temporal%20logic.md) formula.
The main for loop runs for $k$ times. The Boolean cases cost $O(n)$.
The temporal cases cost $O(n+m)$. Hence, the model checker for [CTL](Branching%20time%20temporal%20logic.md) runs in time $O(k \cdot (n + m))$ in the worst-case.
The complexity is linear in the product of the length of the formula and the size of the model.

>[!Wow] This has linear complexity
>This is an amazing result
