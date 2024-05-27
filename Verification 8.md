---
number headings: auto, first-level 1, max 6, 1.1
---

## 0.1 When does the Spoiler always win?
On [[isomorphic|non-isomorpic]] finite structures, Spoiler wins  the Ehrenfeucht Fraise game eventually.

==Why? ==
Due to the __finite__ amount of elements in the structure at some point all elements of one of the two structures will be selected. Then, due to its [[isomorphic|non-isomorphic]] nature a ==element that is not present in one of the two structures will be chosen==.  In that moment the <mark style="background: #FF5582A6;">Spoiler</mark> wins as the <mark style="background: #014E11F2;">Duplicator</mark> can not chose the element as it is not present.

> [!note] A measure of similarity [[remoteness]]
> How long the duplicator survies in the game is a measure of how simmilar two structures are. The longer he survives the more simmilar the structures are.
> 

But there are quicker ways of wining for the spoiler. For instance by the tactic divide and conquer:

### 0.1.1 Examples
==Board==
![[Verification 8_image_1.png|700]]

==Turn one==
<mark style="background: #FF5582A6;">Spoiler:</mark> 
Chooses a node exactly in the middle of all the nodes in $S$.

<mark style="background: #014E11F2;">Duplicator:</mark> 
Reacts by choosing the middle point of $S'$.

==next Turns==
The <mark style="background: #FF5582A6;">spoiler</mark> divides the nodes every turn further. The <mark style="background: #014E11F2;">duplicator</mark> has to respond by dividing $S'$ until eventually on the side the <mark style="background: #FF5582A6;">spoiler</mark> plays there exists a node between two nodes and on the side the <mark style="background: #014E11F2;">duplicator</mark> plays there is no node that is between those two nodes and he fails. This tactic has __logarithmic runtime__ in relation to the number of nodes i.e. log(n) with n being the number of nodes.

![[Verification 8_image_2.png| Second turn both sides choosing the middle node]]

![[Verification 8_image_3.png| Consecutive turns halfing the nodes more and more]]

## 0.2 Are there structures where the Duplicator can survive an arbitrary amount of rounds but not infinitely?

### 0.2.1 Example
==Board:==
![[Verification 8_image_4.png]]

$S=(\mathbb{Z},<)$ are the ordered natural numbers.
$S'=(\{1,2\}\times \mathbb{Z},<_{lex})$ are two sets of ordered natural numbers. One note: If two nodes are in different sets of the natural numbers their ordering still holds. Nodes that are further right have a higher value than values on the left. The lex stands for [[lexicographic ordering]].

==Turn one:==
The Spoiler choose a node in $S'$. And The duplicator responds by choosing a node in $S$
![[Verification 8_image_5.png]]
==Turn two:==
Maybe Spoiler chooses a node right next to the first node it set. Duplicator can still respond.
![[Verification 8_image_6.png]]

==Turn three:==
The Spoiler chooses now a node on the other set of $\mathbb{Z}$. Now the Duplicator has in his hand how long he will survive. Depending on how far away he puts his node away from his first two nodes the longer he will survive. But not infinitely. 
![[Verification 8_image_7.png]]

==In the following turns==
The spoiler will now using the tactic he used in the previous example: Divide and conquer. He will try to set the dividing stone on the second set of $\mathbb{Z}$ one further away from the middle than it is possible for the Duplicator. Then by halving the distance at some point the Spoiler will be able to go on dividing while the Duplicator can not.  Then the duplicator looses.

==Take away:==
Depending on how far away from his first two choices the duplicator choose his 3rd node he will survive longer or less long. He can survive n rounds depending on his chosen distance between the nodes. But eventually he loses. This is meant by [[#Are there structures where the Duplicator can survive an arbitrary amount of rounds but not infinitely]].

Question: Why can the Spoiler not just choose a element twice. Like the second choice and then the same node in the other set of $\mathbb{Z}$? Would this also not be isomorphic then?


# 1 The Fraisse Ehrenfeucht theorem [[Theorem 1]]
We introduce [[Theorem 1]].
> [!note] Theorem 1
> $S$ and $S'$ are [[n-equivalence|n-equivalent]] $\iff$ the Duplicator survives n-rounds in the [[Ehrenfeucht-Fraise game]] $G_{S,S'}$
> 

Lets remember [[Lemma 10]]:
> [!note] Lemma 10
> If there are two structure $S,S'$ such that:
> $S \in P$ and $S\notin P$ and $S$ and $S'$ are [[n-equivalence|n-equivalent]] then $\text{\textcolor{red}{P is not definable in First order logic}}$

When we combine [[Theorem 1]] and [[Lemma 10]] we can substitute the "''are [[n-equivalence|n-equivalent]]" by "n-rounds in the [[Ehrenfeucht-Fraise game]] $G_{S,S'}$". By this we can prove even better if a Property is definable in [[FO - First order logic|FO]]

What does this mean for our example above?

The property $P=${every two points are at a finite distance} is __not__ definable in [[FO - First order logic|FO]] since $S \in P$ but $S' \not \in P$. The reasoning is the following:
	As all points are at a finite distance from each other in $S=(\mathbb{Z},<)$ but  there exist two points in $S'=(\{1,2\}\times \mathbb{Z},<_{lex})$ where the distance between those is infinite. For instance the points $\{\emptyset,1\}$ and $\{1,\emptyset\}$ where the first only has an element in  $\mathbb{Z}_2$ and the second has only an element in $\mathbb{Z}_1$

## 1.1 Example:
P={Connected Graphs}
Question: given $n$ find $S\in P$ and $S \not \in P$ where the duplicator can survive n rounds.

One structure which is a connected graph is the following and will be our $S$. The __size of our circle depends on the n__ which we can freely choose beforehand:

![[Verification 8_image_8.png|400]]


The Structure $S'$ that does not fulfill the property P is are two not connected graphs:

![[Verification 8_image_9.png|600]]

==Turn 1:==
In the turn one Spoiler and Duplicator start in the same way.
![[Verification 8_image_10.png]]

==Turn 2==
Now we do the obligatory move as before. The Spoiler chooses a second node on the first circle and the Duplicator responds.
![[Verification 8_image_11.png]]

==Turn three== 
Now the Spoiler chooses a node on the second circle. Now the Duplicator is in trouble he will choose a node on the first circle that is as far as possible away from the first two chosen nodes that it gets unveiled as late as possible that the two structures are the same.

![[Verification 8_image_12.png]]

==The remaining n turns:==
The Spoiler will engage again into the tactic of divide and conquer cutting the distance between the nodes 3 and 2 always in half. After $log(nr\_nodes/2)$ turns there will be a two nodes that are right next to each other on the left, but there will be another node in circle two then the Spoiler will win.

This means that the property of [Connectedness](Connectedness.md) i.e. P={Connected Graphs} is not definable in [[FO - First order logic|FO]].

We anticipated this already in the previous classes as to define [[Connectedness]] [[FO Resolution]] would need some kind of principle of induction


 This can be proven by a connection of [[Lemma 10]] and [[Theorem 1]].
 
## 1.2 Example:
 We want to prove if the property $P=${has even cardinally} is definable in [[FO - First order logic|FO]]. A variable $n$ is given and defines the size of our structure $S$ and $S'$.  We try to find two structures where $S\in P$ but $S'\not \in P$ and in the a [[Ehrenfeucht-Fraise game]] survives n rounds.
 
 ==Board==
 We have two structures with a even number of elements $S$ ($2^n$) and a structure $S'$ with an uneven number of elements ($2^n+1$)
![[Verification 8_image_13.png|600]]

==Turn 1==
 The first turn happens like always. The Spoiler chooses the very left node, the Duplicator chooses the very left node to respond
![[Verification 8_image_14.png|600]]

==Turn 2==
Now the Spoiler plays a pebble to the left of the first pebble he played in $S$. Then the duplicator responds by choosing a node that is as far away as possible from the first chosen node position in $S'$. Hereby the distance between $1$ and $2$ in $S$ is even while in $S'$ the number of elements between $1$ and $2$ is uneven.
![[Verification 8_image_15.png|600]]

==Turn 3==
From turn 3 on the Spoiler changes each turn between $S$ and $S'$ to force the Duplicator to choose nodes that are closer and closer to the initial node he choose.
![[Verification 8_image_16.png|600]]

==The following turns:==
The gab between the nodes get smaller and smaller at some point we see that the two two chains are not the same b

>[!Question] 
> why does the Spoiler not do Divide and conquer?
> why is the game not always over after 3 rounds as the Spoiler chooses how far the second chosen node is away from the first chosen node?

> [!note] rule of Thumb: how should the duplicator respond?
> If the Spoiler plays "close" to the previouse pebbles the Duplicator should respond __isomorpically__ (on the same node in the other structure) within the corresponding neighbourhoods.Otherwise the Duplicator will play "far" but has therefore freedom of choice.


Other examples of properties not definable in [[FO Resolution]] are:
1. [[Connectedness]]
2. [[finiteness]]
3. [[parity]] (even/odd)
4. [[2-colorability]]
5. [acyclicity](acyclicity)
 
 
  Example: [[finiteness]]
 $S=\mathbb{Z}$
 $S'=\mathbb{Z},-\mathbb{Z}$
 
 $S$ is the set of natural numbers.
 $S'$ is the set of Natural numbers concatenated with a set of negative natural numbers.
 
 The spoiler wins when he is able to force the Duplicator to choose the first element of the $-\mathbb{Z}$ as in $S$ the vertices left are always valued less than the vertices right. But at the point where $\mathbb{Z}$ and $-\mathbb{Z}$ meet we have that the left element is valued more than the vertice one further right.
 
 >[!Question]
 >Why not choose a finite set of nodes  ($2^n$) and a infinite set of nodes ($\mathbb{Z}$) and then do divide and conquer. The duplicator can survive depending on how high the number n is.
 
 Example: [[acyclicity]] 
 $S$ = a circle Graph
 $S'$ = ($\mathbb{Z},+1$) -> +1 is successor relation.
 
 >[!Rule of thumb]
 >The two structures have to always look the same locally. That is why a finite line is not serving well in the example for [[acyclicity]] because the endnotes do not look similar to any other node in $S$.
 
 
# 2 Proof [[Theorem 1]]:

 >[!Note] [[Theorem 1]]
 >$S$ and $S'$ are [[n-equivalence|n-equivalent]] $\iff$ the Duplicator survives n-rounds in the [[Ehrenfeucht-Fraise game]] $G_{S,S'}$

 
 We will prove it from left to right. First starting with the definition of [[n-equivalence]]
 
 >[!Note] [[n-equivalence]]
 $S,S'$ are n-equivalent if for every $\phi$ with [[Quantifier rank]] n the following holds true: $S \models \phi \iff S' \models \phi$

 
 Now we can reinterpret the statement $S \models \phi$ and $S' \models \phi$ into a game theoretical term. How do we do [[Model-checking]] using a game: With the [[The evaluation game]]. That means $S \models \phi$ if Eve has a [[Strategy]] to win the [[The evaluation game]] $G_{S,\phi}$ every time. The same is true for $S'$: if Eve wins the [[The evaluation game]] $G_{S',phi}$ every time it follows that $S \models \phi$. 
 
 So now we have three Games:
 - The [[The evaluation game]] $G_{S,\phi}$
 - The [[The evaluation game]] $G_{S',\phi}$
 - The [[Ehrenfeucht-Fraise game]] $G_{S,S'}$

Now that we have defined the Theorem in game theory terms we will use [[Induction]] to prove [[Theorem 1]].


## 2.1 1. part of proof from duplicator survives n rounds $to$ n-equivalence
We rewrite the statement of what we want to prove:
We have a formula $\phi$ with [[Quantifier rank]] n. We have a Structure $S$ that models $\phi$ ($S \models \phi$)  and the <mark style="background: #014E11F2;">Duplicator</mark> survives n rounds in $G_{S,S'}$.

Now we only need to prove that  $S'$ models $\phi$ if and only if the above conditions are met.


There are four cases in which we can split up a formula:
- [[#2 1 Disjunction]]
- [[#2 2 Conjunction]]
- [[#2 3 Existential quantification]] 
- [[#2 4 Universal quantification]]

## 2.2 Disjunction
A disjunction is $\phi = \phi_1 \lor \phi_2$

We do not know first how Eve would play in $G_{S',\phi}$

But using the assumption that Eve has a winning strategy for $G_{S,\phi}$ and she can choose the branch she wants to walk down (either $\phi_1$ or $\phi_2$) she can copy the strategy from $G_{S,\phi}$ to $G_{S',\phi}$ and win as the formulas are the same.

## 2.3 Conjunction
A conjunction is $\phi = \phi_1 \land \phi_2$.

Here we do not have the advantage that Eve can choose the next turn. Adam chooses and we can not influence him.

As we are playing both games in the same manner and we evaluate the same sub-formula we can assume that Adam (even though we do not control him) play the same turns in $G_{S,\phi}$ and $G_{S',\phi}$. This means that we will probably win in the same manner as in $G_{S,\phi}$.

## 2.4 Existential quantification
How does a subformula look if it has a existential quantifier?
$$\exists \phi'(x)$$

When an existential quantifier occurs in  $G_{S,\phi}$ eve bind the free variable to an element in the universe $u \in U^S$.

We would like to transfer this way of doing things directly from $G_{S,\phi}$ to $G_{S',\phi}$   but $u$ is an element of $U^S$ and not of $U^{S'}$.

Therefore we have to use the assumption that the Duplicator survives n rounds from our setup and information from the [[Ehrenfeucht-Fraise game]] $G_{S,S'}$ that is played.

We want to know to which element $v \in U^{S'}$ we need to bind to still win the evaluation game. Therefore we look at how the [[Ehrenfeucht-Fraise game]] plays out.

The spoiler will choose the pebble $u \in U^S$ to which the variable $x$ has been bound in [[The evaluation game]]. Then we look with which pebble the Duplicator responds to. He chooses a element v. We take this information and bind the variable $x$ in the game $G_{S',\phi}$ to the chosen element $v$ that was previously chosen by the Duplicator in the [[Ehrenfeucht-Fraise game|EF-game]]. This can be seen in the figure below.
![[Verification 8_image_17.png|500]]

Why does this work? As the duplicator tries to maintain partial [[isomorphic|isomorphism]] the elements $v$ and $u$ are equivalent.

## 2.5 Universal quantification
The universal quantification looks like this:
$$\forall x \phi(x)$$

When having a universal quantifier Adam chooses which element $v \in U^{S'}$ he binds to x. 
To figure out how we have to react in the evaluation game we use the [[Ehrenfeucht-Fraise game|EF-game]] in the other direction. We let Spoiler choose the pebble $v \in S'$. Then the Duplicator responds with a pebble $u \in S$.  We then choose the element $u$ chosen by the duplicator in our [[The evaluation game|evaluation game]] $G_{S'\phi}$. Because the duplicator wants to maintain partial [[isomorphic|isomorphism]] we know that the chosen $u$ and $v$ are equivalent and hereby we can be sure that we also win  $G_{S,\phi}$. (see image)

![[Verification 8_image_18.png|500]]

> [!note] How many rounds can we use the [[Ehrenfeucht-Fraise game|EF-game]] to help us bind the elements in the [[The evaluation game|evaluation game]]?
> As we know that the duplicator can only survive n rounds we can use the [[Ehrenfeucht-Fraise game|EF-game]] only for n nested quantifications.
> 
> This is where the precondition comes from that our formula has at most [[Quantifier rank]] n.

==With this first part of the prove we only showed one direction of the $\iff$. (i.e. n-equivalent $\to$ Duplicator survives n rounds) Now we have to show the other direction==

## 2.6 part of proof from n-equivalence $\to$ Duplicator survives n rounds.

> [!note] What do we have to prove?
> Supposing $S,S'$ are [[n-equivalence|n-equivalent]] (for every formular $\phi$ with [[Quantifier rank]] n the following must be true: $S\models \phi \iff S' \models \phi$) we have to find a strategy for the Duplicator in th [[Ehrenfeucht-Fraise game]] to survive n rounds.

What is one problem that we face? We have a $\forall$ in the definition of the [[n-equivalence]]. S and S' must model every formula $\phi$ with quantifier rank smaller or equal $n$.

To proof the assumption we need a $\phi$ that is strong enough to cover all cases of the duplicator. We need a formula that is stronger than all other formulas with [[Quantifier rank]] n to make assumptions over all formulars with [[Quantifier rank]] n.

Therefore we introduce the [[Hintikka Formula]].

## 2.7 [[Hintikka Formula]] 

The [[Hintikka Formula]] $\phi_S^n$ is defined by the [[Quantifier rank]] n as well as for one of the Structures S or S' 

Intuitive definition: 
The strongest formula with [[Quantifier rank]] n that holds on the structure $S$ (i.e. $S \models \phi$ ).

Definition over [[FO Resolution]]
The [[FO - First order logic|First order logic]] of $S$ relativised to [[Quantifier rank]] n.

with other words:  The first order logic of S is all formulas $\phi$ that mode $S$. With relativised we mean that we only take the formulas that have a [[Quantifier rank]] smaller or equal $n$.

in mathematical writing:
A [[Conjunction]] of all formulas n that have a [[Quantifier rank]] smaller or equal $n$ that model $S$ i.e. $\bigwedge \{\phi(q.r. n) : S \models \phi\}$

Problem: this is a infinite [[Conjunction]] which is not possible in [[FO - First order logic]]

### 2.7.1 We can define the [[Hintikka Formula]] inductively on $n$:

==Induction start with $n=0$

$$\phi_S^0= \bigwedge \alpha \land \bigwedge \neg \beta$$

$\alpha$ and $\beta$ are [[atomic]] meaning it does not have free variables for instance $R()$.

- $\alpha$ are all formulas which are modeled by $S$ i.e. $S \models \alpha$
- $\beta$ are all formulas that do not model $S$ i.e. $S \not \models \beta$. Therefore we have a $\neg$ infront of $\beta$ in the definition of $\phi_S^0$ to make it be modeled by $S$.

==induction step==

$$\phi_S^n= \bigwedge\limits_{\substack{u \in U^S\\S_u=S[x:=u]}} \exists x \quad \phi_{S_{u}}^{n-1} \quad \land \forall x\bigvee\limits_{\substack{u \in U^S\\S_u=S[x:=u]}} \quad \phi_{S_{u}}^{n-1}$$

In the first part of the Formula. We take the  an element $u$ of $U^S$ and assign it to a free variable x creating the structure $S_u$. By now asking if there exists a $x$ so that the formula is true we make the formula true (==I am not sure how this works==). The same happens for the second part of the formula again we take the  an element $u$ of $U^S$ and assign it to a free variable x creating the structure $S_u$ with the only difference that we convert the $\bigwedge \neg$ into $\forall x \bigvee$ which are equivalent.

Question: how does this work? No idea.

Now that we have found the [[Hintikka Formula]] which is the strongest formula of all formulas of [[Quantifier rank]] n we have to find a [[Strategy]] for the duplicator to survive n rounds.


### 2.7.2 Spoiler plays in $S$ in the [[Ehrenfeucht-Fraise game|EF-game]] 

When the Spoiler chooses an element $u$ in the [[Ehrenfeucht-Fraise game|EF-game]] we need to find out how the Duplicator needs to respond so that he survives for n rounds.

Therefore we look at how the players of the [[The evaluation game|evaluation games]] $G_{S,\phi}$ and $G_{S',\phi}$ play.

In the game $G_{S,\phi}$ for the first turn Adam at the branch with the $\land$ choose the left side of the equation i.e. $\bigwedge\limits_{\substack{u \in U^S\\S_u=S[x:=u]}} \exists x \quad \phi_{S_{u}}^{n-1}$ in the second turn he will choose $\exists x \quad \phi_{S_{u}}^{n-1}$. In the second game $G_{S',\phi}$ Adam will choose the same path down the [[Tableaux]] i.e. first $\bigwedge\limits_{\substack{u \in U^S\\S_u=S[x:=u]}} \exists x \quad \phi_{S_{u}}^{n-1}$, then $\exists x \quad \phi_{S_{u}}^{n-1}$. 

Eve on the other side  in game $G_{S,\phi}$  will bind $x$ to $u$ and in the game $G_{S',\phi}$ x will be bound to $v$ which also leads to the response of the duplicator.

The Duplicator will choose the by Eve chosen node $v$

![[Verification 8_image_19.png|500]]

### 2.7.3 Spoiler plays in $S'$ in the [[Ehrenfeucht-Fraise game|EF-game]] 
Initially Spoiler places a pebble $v \in U^{S'}$.
At the start we can reason in a similar way as if spoiler would play in $S$ as described in the chapter above.

In the [[The evaluation game|evaluation game]] $G_{S',\phi}$ he picks the right conjunction i.e. $\forall x \bigvee\limits_{\substack{u \in U^S\\S_u=S[x:=u]}} \phi_{S_{u}}^{n-1}$.  He binds $x$ to some variable $v$ which is the same variable as the  Spoiler choose in the [[Ehrenfeucht-Fraise game|EF-game]].

As we know that $S' \models \phi_S^n$ for as it is equivalent for formulas of [[Quantifier rank]] n because of [[n-equivalence]]. That means Eve will choose one of the paths at a disjunction without losing because she has a winning strategy for at least n turns. She goes down a path to find the formula $\phi_{S_{u}}^{n-1}$ .  With this she already highlights how the duplicator should respond.

The duplicator responds by choosing the  $u \in U^s$ that Eve chooses in the [[The evaluation game|evaluation game]]. 

Hereby we have a complete tactic for the [[Ehrenfeucht-Fraise game|EF-game]] but we still need to find a way to let the two [[The evaluation game|evaluation games]] we run, run synchronously.

The response of Adam in the [[The evaluation game|evaluation game]] $G_{S,\phi}$ the response is straight forward. He chooses the same conjuction as the Adam in the other evaluation game but bind $x$ to the $u$ Eve has chosen.

As we also know that $S \models \phi_S^n$ for as it is equivalent for formulas of [[Quantifier rank]] n because of [[n-equivalence]]. That means Eve can savely choose the
disjunct $\phi_{S_u}^{n-1}$ for n turns without losing.

![[Verification 8_image_20.png|500]]

### 2.7.4 To Summarize:
We proofed [[Theorem 1]]:
$S$ and $S'$ are [[n-equivalence|n-equivalent]] $\iff$ the Duplicator survives n-rounds in the [[Ehrenfeucht-Fraise game]] $G_{S,S'}$ i.e.  $\iff$ the [[Hintikka Formula]]s $\phi_S^n$ and $\phi_{S'}^n$ are logically equivalent.

What can we learn from this:
1. $\phi_n^S$ can be used as a representant of [[n-equivalence|n-equivalence]] class of $S$
2. For every formula $\phi'$ of [[Quantifier rank]] n the following statement holds true:
	$$\phi'\in FO[S] \iff \phi' \text{ is a logical consequence of } \phi_S^n$$
	
	In easy words this means that $\phi'$ can be expressed in [[FO - First order logic|FO]] if one can construct $\phi'$ from a disjunction of [[Hintikka Formula]]s $\phi_S^n$ 

# 3 [Synthesis Problem](Synthesis%20Problem.md)

We have a reachability problem i.e. we have $k$ bits in one configuration of 1's and 0's and we want to know if there is a formula that we can reach another configuration of bits.

Here with [Synthesis Problem](Synthesis%20Problem.md) it gets a bit more complicated. We do not have full control over all bits just about a subset of $l$ bits while $l<k$ while k is the number of bits.

The question is now can we reach our configuration independently of how the environment influences the bits that we do not have control over?

![[Verification 8_image_21.png]] 


A tiny bit more formally:
-  we control the bits $\bar{p_i}$ <mark style="background: #014E11F2;">green</mark> 
-  the environment (we do not have any control over them) controlls the bits $\bar{q_i}$ (<mark style="background: #FF5582A6;">red</mark> ).

We could represent it in a [[QBF]] formula like this:
$$\forall \bar{q_1}\exists\bar{p_1}...\forall \bar{q_{k-l}}\exists\bar{p_l}\phi_{path}(\bar{q_1}\bar{p_1}... \bar{q_{k-l}}\ \bar{p_l})$$

Then one can run a [[The evaluation game|evaluation game]] to check if the formula is fulfilable independent of the bits we do not control.

Now the question is what happens when we do not know the exact number of bits overall bits: then we can not express the formula in [[QBF]]. Then we use [[automata]] to evaluate if one can fullfil the synthesis.

# 4 Things to remember
- [[Ehrenfeucht-Fraise game|EF-game]] are a powerful tool to study [[Definability]] in [[FO - First order logic|FO]].

it works like this:
1. Find a property P and $n \in \mathbb{N}$
2. find two models $S \in P$ and $S\notin P$ which depend on n
3. show that the Duplicator has a strategy to survive n rounds in $G_{S,S'}$ -> [[n-equivalence]] 
4. Then it follows that $P$ is not definable in [[FO - First order logic|FO]].

The [[Ehrenfeucht-Fraise game|EF-game]] can also be easily adapted to other logics and problems