---
number headings: auto, first-level 1, max 6, 1.1
---

#Remember 
# 1 Things to remember 
- [[FO - First order logic]] is powerful and expressive 
- Model-checking is decidable (in [[PSPACE]]) when the universe is finite.
- [[Satisfiability]],[[Validity]],[[logical equivalence]] are all undecidable (proven a by the [[Turing machine]] to [[Domino-Problem]] reduction)
- For infinite universes one ca fix a model and study its [[FO-theories|FO-Theory]]. Some [[FO-theories]] are decidable some not.
- Some [[FO-theories]] can be compared to other [[FO-theories]] using [[Logical reduction]]

# 2 Games in Logic 
Goal: check which properties/ languages are *definable* in logic (for instance [[FO - First order logic]])

==Examples:==
- Is the property "Universe has even [[Cardinality]]" definable in [[FO - First order logic]]?
- Is the class of "Strongly connected graphs" definable in [[FO - First order logic]] using edges? (Not possible in [[FO - First order logic]])
- Is the language $L=(AA)*$ definable in [[FO - First order logic]] using $\leq$ (Not possible in [[FO - First order logic]])
> meaning: $L=(AA)*$ is the set of all finite strings that have even length

<mark style="background: #FF5582A6;">Problem:</mark> If we want to prove one of this properties it is very easy to proof if it is possible to prove. We write down the formula, check if it says what we want it says and it is done. 
It is different though if we can not find a prove. It is very difficult to show that something is not possible. 

## 2.1 [[The evaluation game]] also known as model checking game 
__GOAL__: check whether $s \models \phi$

Example:
[[The evaluation game]] for  [[QBF]] 
input: $\phi$ 
e.g. : $\forall p \exists q \forall r (p \lor \neg q) \land (r \lor q)$

The Structure $S=\emptyset$

==Question:== $S \overset{?}{\models} \phi$

Now we use a [[Tableaux]] tree structure back from [[Verification 3]] to see if the formula is valid. We add $\forall$ and $\exists$.

This is the first picture of the [[Tableaux]]. We start with a $\forall$. If there is a $\forall$ every branch has to be positive. This is every node that has red text color. The nodes with $\exists$ have green text color and there only one of the branches needs to be $True$.

After the branches with the $\exists$ and $\forall$ we have to append the <mark style="background: #014E11F2;">tree bottom</mark> at every position that has a $'*'$ in the <mark style="background: #014E11F2;">tree top</mark> .

<mark style="background: #014E11F2;">Tree top:</mark> 
<!-- https://q.uiver.app/?q=WzAsMTYsWzQsMCwiXFx0ZXh0Y29sb3J7cmVkfXtcXGZvcmFsbCBwfSJdLFs1LDEsIlxcdGV4dGNvbG9ye2dyZWVufXtcXGV4aXN0cyBxfSJdLFszLDEsIlxcdGV4dGNvbG9ye2dyZWVufXtcXGV4aXN0cyBxfSJdLFsxLDIsIlxcdGV4dGNvbG9ye3JlZH17XFxmb3JhbGwgcn0iXSxbMywyLCJcXHRleHRjb2xvcntyZWR9e1xcZm9yYWxsIHJ9Il0sWzUsMiwiXFx0ZXh0Y29sb3J7cmVkfXtcXGZvcmFsbCByfSJdLFs3LDIsIlxcdGV4dGNvbG9ye3JlZH17XFxmb3JhbGwgcn0iXSxbMCwzLCIqIl0sWzEsMywiKiJdLFsyLDMsIioiXSxbMywzLCIqIl0sWzUsMywiKiJdLFs2LDMsIioiXSxbNywzLCIqIl0sWzgsMywiKiJdLFs4LDJdLFswLDEsInA9MSIsMV0sWzAsMiwicD0wIiwxXSxbMiwzLCJxPTAiLDFdLFsyLDQsInE9MSIsMV0sWzEsNSwicT0wIiwxXSxbMSw2LCJxPTEiLDFdLFszLDddLFszLDhdLFs0LDldLFs0LDEwXSxbNSwxMV0sWzUsMTJdLFs2LDEzXSxbNiwxNF1d --> <iframe class="quiver-embed" src="https://q.uiver.app/?q=WzAsMTYsWzQsMCwiXFx0ZXh0Y29sb3J7cmVkfXtcXGZvcmFsbCBwfSJdLFs1LDEsIlxcdGV4dGNvbG9ye2dyZWVufXtcXGV4aXN0cyBxfSJdLFszLDEsIlxcdGV4dGNvbG9ye2dyZWVufXtcXGV4aXN0cyBxfSJdLFsxLDIsIlxcdGV4dGNvbG9ye3JlZH17XFxmb3JhbGwgcn0iXSxbMywyLCJcXHRleHRjb2xvcntyZWR9e1xcZm9yYWxsIHJ9Il0sWzUsMiwiXFx0ZXh0Y29sb3J7cmVkfXtcXGZvcmFsbCByfSJdLFs3LDIsIlxcdGV4dGNvbG9ye3JlZH17XFxmb3JhbGwgcn0iXSxbMCwzLCIqIl0sWzEsMywiKiJdLFsyLDMsIioiXSxbMywzLCIqIl0sWzUsMywiKiJdLFs2LDMsIioiXSxbNywzLCIqIl0sWzgsMywiKiJdLFs4LDJdLFswLDEsInA9MSIsMV0sWzAsMiwicD0wIiwxXSxbMiwzLCJxPTAiLDFdLFsyLDQsInE9MSIsMV0sWzEsNSwicT0wIiwxXSxbMSw2LCJxPTEiLDFdLFszLDddLFszLDhdLFs0LDldLFs0LDEwXSxbNSwxMV0sWzUsMTJdLFs2LDEzXSxbNiwxNF1d&embed" width="1200" height="560" style="border-radius: 8px; border: none;"></iframe>

<mark style="background: #014E11F2;">Tree bottom: </mark> 
<!-- https://q.uiver.app/#?q=WzAsOCxbMSwwLCJcXHsgKHAgXFxsb3IgXFxuZWcgcSkgXFxsYW5kIChyIFxcbG9yIHEpIFxcfSJdLFsxLDEsIlxce3AgXFxsb3IgXFxuZWcgcSxyIFxcbG9yIHFcXH0iXSxbMSwyLCJcXHtwLHIgXFxsb3IgcVxcfSJdLFsyLDIsIlxce1xcbmVnIHEsciBcXGxvciBxXFx9Il0sWzEsMywiXFx7cCxxXFx9Il0sWzIsMywiXFx7XFxuZWcgcSxyXFx9Il0sWzAsMywiXFx7cCxyXFx9Il0sWzMsMywiXFx7XFxuZWcgcSxxXFx9Il0sWzAsMV0sWzEsMl0sWzEsM10sWzIsNF0sWzMsNV0sWzIsNl0sWzMsN11d --> <iframe class="quiver-embed" src="https://q.uiver.app/#?q=WzAsOCxbMSwwLCJcXHsgKHAgXFxsb3IgXFxuZWcgcSkgXFxsYW5kIChyIFxcbG9yIHEpIFxcfSJdLFsxLDEsIlxce3AgXFxsb3IgXFxuZWcgcSxyIFxcbG9yIHFcXH0iXSxbMSwyLCJcXHtwLHIgXFxsb3IgcVxcfSJdLFsyLDIsIlxce1xcbmVnIHEsciBcXGxvciBxXFx9Il0sWzEsMywiXFx7cCxxXFx9Il0sWzIsMywiXFx7XFxuZWcgcSxyXFx9Il0sWzAsMywiXFx7cCxyXFx9Il0sWzMsMywiXFx7XFxuZWcgcSxxXFx9Il0sWzAsMV0sWzEsMl0sWzEsM10sWzIsNF0sWzMsNV0sWzIsNl0sWzMsN11d&embed" width="891" height="560" style="border-radius: 8px; border: none;"></iframe>

Question: How do we evaluate the tree? What happens if there is a contradiction like in this tree.


This is very similar to a game ([[2-player game]])


### 2.1.1 [[2-player game]]
[[Player]]:
- $\textcolor{red}{\text{Adam }(\forall,\land)}$ in literature called  __Verifyer__
- $\textcolor{green}{\text{Eve }(\exists,\lor) }$ in literature called __Falsifier__

One game can have multiple rounds. One __round__ of the game consists of Adam and Eve choosing branches of the node (either go left or right) taking turns. $\textcolor{red}{Adam}$ chooses whenever there is a $\forall$ or a $\land$, $\textcolor{green}{Eve}$ chooses when there is a $\exists$ or a $\lor$. The round ends when they have reached the end of a branch i.e. a leaf of the tree.

What is the <mark style="background: #014E11F2;">goal</mark> ?
> Eve wants to find a [[Strategy]] that allows her to reach a $True$ leaf (of the board) no matter what Adam does!

[[Board]] / Arena:
Is a tree or a graph might be finite or infinite. In our case it is the tree that we drew above.

What is the point? What is behind this?
We want to check if a formula holds on a Structure! Here we have a Lemma!

[[Lemma 8]]:
$S \models \phi \iff$ Eve has a [[Strategy]] where she always wins the game over the board $G_{\phi,S}$

==Example:==

$$\phi = \forall p \exists q (p \land \neg q) \lor (\neg p \land q)$$

Our structure $S$ is empty because we do not have free variables. $S= \emptyset$

What is the board:
Upper tree:
<!-- https://q.uiver.app/?q=WzAsNyxbMiwwLCJcXGZvcmFsbCBwIl0sWzEsMSwiXFxleGlzdHMgcSJdLFszLDEsIlxcZXhpc3QgcSJdLFswLDIsIioiXSxbMSwyLCIqIl0sWzMsMiwiKiJdLFs0LDIsIioiXSxbMCwxLCJwPTAiLDIseyJjb2xvdXIiOlswLDYwLDYwXX1dLFswLDIsInA9MSIsMCx7ImNvbG91ciI6WzAsNjAsNjBdfV0sWzEsMywicT0wIiwxLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV0sWzEsNCwicT0xIiwwLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV0sWzIsNSwicT0wIiwxLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV0sWzIsNiwicT0xIiwwLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV1d --> <iframe class="quiver-embed" src="https://q.uiver.app/?q=WzAsNyxbMiwwLCJcXGZvcmFsbCBwIl0sWzEsMSwiXFxleGlzdHMgcSJdLFszLDEsIlxcZXhpc3QgcSJdLFswLDIsIioiXSxbMSwyLCIqIl0sWzMsMiwiKiJdLFs0LDIsIioiXSxbMCwxLCJwPTAiLDIseyJjb2xvdXIiOlswLDYwLDYwXX1dLFswLDIsInA9MSIsMCx7ImNvbG91ciI6WzAsNjAsNjBdfV0sWzEsMywicT0wIiwxLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV0sWzEsNCwicT0xIiwwLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV0sWzIsNSwicT0wIiwxLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV0sWzIsNiwicT0xIiwwLHsiY29sb3VyIjpbMTIwLDYwLDYwXX0sWzEyMCw2MCw2MCwxXV1d&embed" width="688" height="432" style="border-radius: 8px; border: none;"></iframe>
Lower tree:

<!-- https://q.uiver.app/?q=WzAsNSxbMiwwLCJcXHsocCBcXGxhbmQgXFxuZWcgcSkgXFxsb3IgKFxcbmVnIHAgXFxsYW5kIHEpXFx9Il0sWzAsMSwiXFx7XFx7IChwIFxcbGFuZCBcXG5lZyBxKSBcXH0iXSxbNCwxLCJcXHsoXFxuZWcgcCBcXGxhbmQgcSlcXH0iXSxbMCwyLCJcXHtwLFxcbmVnIHFcXH0iXSxbNCwyLCJcXHtcXG5lZyBwLHFcXH0iXSxbMCwxXSxbMCwyXSxbMSwzXSxbMiw0XV0= --> <iframe class="quiver-embed" src="https://q.uiver.app/?q=WzAsNSxbMiwwLCJcXHsocCBcXGxhbmQgXFxuZWcgcSkgXFxsb3IgKFxcbmVnIHAgXFxsYW5kIHEpXFx9Il0sWzAsMSwiXFx7XFx7IChwIFxcbGFuZCBcXG5lZyBxKSBcXH0iXSxbNCwxLCJcXHsoXFxuZWcgcCBcXGxhbmQgcSlcXH0iXSxbMCwyLCJcXHtwLFxcbmVnIHFcXH0iXSxbNCwyLCJcXHtcXG5lZyBwLHFcXH0iXSxbMCwxXSxbMCwyXSxbMSwzXSxbMiw0XV0=&embed" width="700" height="300" style="border-radius: 8px; border: none;"></iframe>

---

Now we evaluate the turns $\textcolor{green}{Eve}$ can do to counter $\textcolor{red}{Adam}$.

Due to our way to paint the graph the $\textcolor{red}{Adam}$ chooses at the $\forall$ and $\textcolor{green}{Eve}$ chooses the way at the $\exists$. The choice of $\textcolor{red}{Adam}$ at the $\land$ is symbolized by the fact that a leave has to have all entries *True* to count as *True*.

First what happens if $\textcolor{red}{Adam}$ chooses the left branch and sets $p=0$

$\textcolor{green}{Eve}$ has two options. First we look what happens when she chooses the left branch setting $q=0$. As already noted before $\textcolor{green}{Eve}$ controls the $\lor$ meaning she can choose at the crossings in the <mark style="background: #014E11F2;">lower tree</mark>  where to go. If she finds a way to a *True* leaf the entire evaluation is counted as *True*.

> $p=0,q=0$
> - left branch: $\{p=0,\neg q = 1\} \to \text{False}$
> - right branch: $\{\neg p=1, q = 0\} \to \text{False}$
> As both leafs are *False* the $\textcolor{green}{Eve}$ does not have a choice and this branch is counted as *False*. 

Now we look at the other option of $\textcolor{green}{Eve's}$ the right branch setting $q=1$
> $p=0,q=1$
> - left branch: $\{p=0,\neg q = 0\} \to \text{False}$
> - right branch: $\{\neg p=1, q = 1\} \to \text{True}$
> As the second leave is True $\textcolor{green}{Eve}$ always can choose to go to the *True* leave hereby this branch counts as *True*

Concluding if $\textcolor{red}{Adam}$ chooses the left branch and sets $p=0$, $\textcolor{green}{Eve}$ can respond by choosing first the right branch setting $q=1$ and then again the right branch at the first crossing  in the lower tree, hereby finding a way to set the formula *True* and win.

---

What happens if $\textcolor{red}{Adam}$ chooses the right branch and sets $p=1$? 


> $p=1,q=0$
> - left branch: $\{p=1,\neg q = 1\} \to \text{True}$
> - right branch: $\{\neg p=0, q = 0\} \to \text{False}$
> As the first leaf is True $\textcolor{green}{Eve}$ always can choose to go to the *True* leaf, hereby this branch counts as *True*.

Now we look at the other option of $\textcolor{green}{Eve}$ choosing the right branch setting $q=1$.
> $p=1,q=1$
> - $\{p=1,\neg q = 0\} \to \text{False}$
> - $\{\neg p=0, q = 1\} \to \text{False}$
> As both leaves after the crossing are *False* the $\textcolor{green}{Eve}$ does not have a choice and this branch is counted as *False*.

To sum up if $\textcolor{red}{Adam}$ chooses the right branch $\textcolor{green}{Eve}$ can always counter by choosing the left branch in the upper tree setting $q=0$ and then the left branch to reach a *True* leaf 

---

Summarizing if $\textcolor{red}{Adam}$ chooses the left branch $\textcolor{green}{Eve}$ can counter by choosing the right branch and then the right branch and win.
If $\textcolor{red}{Adam}$ chooses the right branch  $\textcolor{green}{Eve}$ can counter by choosing the left branch and then the left branch again.

This means that  $\textcolor{green}{Eve}$ always has a strategy to win over the board $G_{\phi,S_\emptyset}$! Hereby showing that $S \models \phi$ after [[Lemma 8]].

---

This was an example for [[QBF]]. We could also do  [[The evaluation game]] also for [[FO - First order logic]] the only difference is that the universe does not only contain two elements but $n$ elements meaning that $\textcolor{red}{Adam}$ and $\textcolor{green}{Eve}$ have $n$ possibilities to choose from instead of only two.

### 2.1.2 Formal Definitions for the [[2-player game]]
What do we need:
- We need the formula $\phi$ in [[Negation Normal Form]] (due to a negation swapping the roles of Adam and Eve)

Arena:
> Nodes: are named $\alpha$ and $\lambda$
> - $\alpha$: is a sub-formula of $\phi$
> - $\lambda$ is a binding interpreting the Free variables $\alpha$ into the universe $U_s$

Rules:
First lets look at the easy case: $\alpha$ is a leaf and does not contain $\lor$ or $\land$.
- if $\alpha=R(x_1,...,x_k)$ then the  game ends $\textcolor{green}{Eve}$ wins if $(\lambda(x_1),...\lambda(x_k)) \in R^s$, otherwise $\textcolor{red}{Adam}$ wins. 
	==Meaning:==
	Before we have been in [[QBF]] the we did not have proper relationship symbols. Now the Relationship symbols $R$ are in leafs and need to be applied to our variables $x$ i.e.  $R(x_1,...,x_k)$. Afterwards we interpret the resulting variables $x$ and see if it is part of the interpretation of the relation. For instance the in the [[QBF]] example the interpretation of p i.e. $\lambda(p)$ needed to be equal to one.
- if $\alpha=\neg R(x_1,...,x_k)$ then game ends $\textcolor{red}{Adam}$ wins if $(\lambda(x_1),...\lambda(x_k)) \in R^s$, otherwise $\textcolor{green}{Eve}$ wins.
==Meaning:== the same as above only that the result is negated by the $\neg$ following that $\textcolor{red}{Adam}$ wins
- if $\alpha = \alpha_1 \lor \alpha_2$: then eve can choose which branch to take down the tree. i.e. $\alpha'=\{\alpha_1,\alpha_2\}$ hoping that the chosen branch is *True*. The game continues at $(\alpha',\lambda)$. The tree looks like this and eve can choose which branch to follow down:
<!-- https://q.uiver.app/?q=WzAsMyxbMSwwLCJcXHsoXFxhbHBoYV8xIFxcbG9yIFxcYWxwaGFfMiksXFxsYW1iZGFcXH0iXSxbMCwxLCJcXHtcXGFscGhhXzEsXFxsYW1iZGFcXH0iXSxbMiwxLCJcXHtcXGFscGhhXzIsXFxsYW1iZGFcXH0iXSxbMCwxXSxbMCwyXV0= --> <iframe class="quiver-embed" src="https://q.uiver.app/?q=WzAsMyxbMSwwLCJcXHsoXFxhbHBoYV8xIFxcbG9yIFxcYWxwaGFfMiksXFxsYW1iZGFcXH0iXSxbMCwxLCJcXHtcXGFscGhhXzEsXFxsYW1iZGFcXH0iXSxbMiwxLCJcXHtcXGFscGhhXzIsXFxsYW1iZGFcXH0iXSxbMCwxXSxbMCwyXV0=&embed" width="320" height="152" style="border-radius: 8px; border: none;"></iframe>
- if $\alpha = \alpha_1 \land \alpha_2$: then Adam can choose which branch to take down the tree. i.e. $\alpha'=\{\alpha_1,\alpha_2\}$ hoping that the chosen branch is *False*.  The game continues at $(\alpha',\lambda)$.
- if $\alpha = \exists x \alpha'(x)$ $\textcolor{green}{Eve}$ can choose any element $u$ that is part of the universe $U^s$ ($u \in U^S$) to be assigned (bound) to x, the game continues with at the position $(\alpha',\lambda')$  where $\lambda'= \lambda[x:=u]$ i.e. a variable $x$ gets assigned and element $u$ of the universe $U^S$
-  if $\alpha = \forall x \alpha'(x)$ $\textcolor{red}{Adam}$ can choose any element $u$ that is part of the universe $U^s$ ($u \in U^S$) to be assigned (bound) to x, the game continues with at the position $(\alpha',\lambda')$  where $\lambda'= \lambda[x:=u]$ i.e. a variable $x$ gets assigned and element $u$ of the universe $U^S$ 


---

Break

---

## 2.2 [[Definability]] vs [[elementary equivalence]] vs [[n-equivalence]]

### 2.2.1 [[Definability]]
Sometimes the question is if a certain property $P$ (often expressed in natural language) can be expressed in a certain logic.

Example:
We have a [[Definability]] problem and we express a property in [[Monadic second order logic]], a more complex logic than [[FO - First order logic|FO]]. Now we want to know can we also express this property in [[FO - First order logic]]?

> [!note] Notation:
> $P: \text{ property (i.e. a set of structures)}$
> $S: Structure$
> $\phi: \text{FO formula}$
>  ```
>  
> 1. $P$ __is [[Definability|defined by]]__ $\phi$ if for every $S$ $S \in P \iff S \models \phi$
> 
> ### 2.2.2 [[elementary equivalence]] 
> 1. $S,S'$ [[elementary equivalence|elementary equivalent]] if for every $\phi$:  $S\models \phi \iff S'\models \phi$
> 
> [[elementary equivalence]] is probably called [[elementary equivalence]] because [[FO - First order logic]] was previously called elementary logic.
> ad-note
title: [[Lemma 9]]
If there are two structure $S,S'$ such that:
$S \in P$ and $S\notin P$ and $S$ and $S'$ are [[elementary equivalence|elementary equivalent]] then $\text{\textcolor{red}{P is not definable in First order logic}}$
```

==Proof through contradiction==:
We have $S,S'$ that are [[elementary equivalence|elementary equivalent]] and $S \in P$ and $S\notin P$.

Lets assume we have a property P that is [[Definability|defined by]] $\phi$.

[[Definability| defined by]] means that every Structure $S$ holds:
1. $S \models \phi$
2. $S \in P$

Now we know that $S$ and $S'$ are logically equivalent i.e. for every $\phi$ $S\models \phi \iff S' \models \phi$ 

So that P is definable in [[FO - First order logic]] the following statement needs to hold:
$S \in P \iff S \models \phi \iff S' \models \phi \iff S' \in P$  
But by definition  $S'$ is not part of $P$ i.e. $S' \notin P$ that means this statement cant hold and we found a contradiction resulting in [[Lemma 9]]! 

#### 2.2.2.1 What is the use-case of [[Lemma 9]]?
If we want to prove that a property is not definable than we find two structures S and S' that are elementary equivalent and one fulfills the property and one not. Then we can point at [[Lemma 9]] and have proven that the property is not definable in [[FO - First order logic]].

### 2.2.3 [[Quantifier rank]]
> [!note]
> $\phi$ has [[Quantifier rank]] n if it has at most n nested quantifiers

The number of Quantifiers is  normally  much smaller than the  [[Quantifier rank]].

The [[Quantifier rank]] is smaller or equal the number of Quantifiers.

Example:
$$\phi = \forall x \forall y(\neg R(x,y) \lor (\exists z R(x,z))\lor(\exists t R(t,y)))$$
$\phi$ has [[Quantifier rank]] 3. 

2 Ranks are because of the two Quantifiers $\forall x$ and $\forall y$ which cover the entire formula.

It is only one Rank for $\exists z$ and $\exists t$ as they are on the same level in the formula when looking at the formula in tree form.

One could resolve the formula to the following making the rank clearer:
$$\phi = (\forall x \forall y \quad \neg R(x,y) \lor (\forall x \forall y\exists z \quad R(x,z))\lor(\forall x \forall y\exists t \quad R(t,y)))$$

### 2.2.4 [[n-equivalence]]
> [!note]
> $S,S'$ are n-equivalent if for every $\phi$ with [[Quantifier rank]] n the following holds true: $S \models \phi \iff S' \models \phi$

[[elementary equivalence]] is more strict as [[n-equivalence]].

> [!note] [[Lemma 10]]
> If there are two structure $S,S'$ such that:
> $S \in P$ and $S\notin P$ and $S$ and $S'$ are [[n-equivalence|n-equivalent]] then $\text{\textcolor{red}{P is not definable in First order logic}}$

==NEW GOAL:==
We want to construct a game $G_{S,S'}$ whose winner determines weather S and S' are [[n-equivalence|n-equivalent]]. 

## 2.3 The [[Ehrenfeucht-Fraise game|Ehrenfeucht-Fraise Games]]
==Players:==
- <mark style="background: #014E11F2;">Duplicator</mark> :
> Goal: Wants to prove that $S'$ and $S$ are [[n-equivalence|n-equivalent]]. 
- <mark style="background: #FF5582A6;">Spoiler</mark> :
> Goal: Want to disprove that $S'$ and $S$ are [[n-equivalence|n-equivalent]]



==Arena:==
The arena is a graph. The nodes of the graph are tuples $(u_1,...,u_i,v_1,...,v_i)$ that are chosen from the universe $u_x \in U^S$ and $v_x \in U^{S'}$

One plays __n__ rounds.
At the start there are two empty sets $S|\{\}$ and $S'|\{\}$ who will contain chosen elements of the Spoiler and the Duplicator.

==one round:==
<mark style="background: #FF5582A6;">Spoiler</mark> begins: and chooses an element $u_i$ from the universe $U^S$ or a element $v_i$ from the universe $U^{S'}$ and adds it either to $S|\{\}$ or $S'|\{\}$.

<mark style="background: #014E11F2;">Duplicator</mark> responds: and chooses and element $v_i$ from $U^{S'}$ if <mark style="background: #FF5582A6;">Spoiler</mark> has chosen a element $u_i$ from $U^S$ or by choosing a element $u_i$ from $U^S$ if <mark style="background: #FF5582A6;">Spoiler</mark> has chosen a $v_i$ from $U^{S'}$ and adds it to the sets.

==Who wins?==
The <mark style="background: #014E11F2;">duplicator</mark> wins if after n turns  the two sets (now containing the chosen elements of $u_x$ and $v_x$) $S|\{u_1,...,u_n\}$ and $S'|\{v_1,...,v_i\}$ are [[isomorphic]]

### 2.3.1 Example 1
==Board:==
Two Graphs $S$ and $S'$:
![[Playingfield Ehrenfeucht Fraisse.png|500]]

==First turn:==
The Spoiler chooses a node in $S'$
![[Playingfield Ehrenfeucht Fraisse_1.png|500]]

And the duplicator responds. In this stage of the game he can choose any node. He can't loose. But in this example he chooses the one in the upper left corner node in $S$ because it is similar to the choice of the Spoiler.

![[Playingfield Ehrenfeucht Fraisse_2.png|500]]

The result of this round is that both sets have a single isolated node in them. They are  still isomorphic.

==Second turn==

Now the duplicator chooses another node that is isolated. There are still no nodes that have no connections (edge).

![[Playingfield Ehrenfeucht Fraisse_3.png|500]]

 The challenge for the <mark style="background: #014E11F2;">duplicator</mark> is now to find a node that is also isolated. And he finds one by the node in the lower left corner.
 
 ![[Playingfield Ehrenfeucht Fraisse_4.png|500]]
 
 ==Third turn:==
 
 The <mark style="background: #FF5582A6;">Spoiler</mark> chooses now a third node that is isolated!
 
 ![[Playingfield Ehrenfeucht Fraisse_5.png|500]]
 
 But here the<mark style="background: #014E11F2;"> duplicator </mark> can not respond anymore independent of the choice he does he can not choose a third node that is isolated! ==He loses after two turns!==
 
 <mark style="background: #FF5582A6;">Spoiler</mark> has a strategy to kill the <mark style="background: #014E11F2;">duplicator</mark> in the third rounds! They are only [[n-equivalence|2-equivalent]]
 
 Note: One can also choose the same node twice, but in the example the structure is still different!
 
### 2.3.2 Example 2
==Board:==
Two Graphs $S$ and $S'$:
![[Playingfield Ehrenfeucht Fraisse_6.png|500]]

==Questions to ask:==
- Can the Duplicator survive n rounds e.g. 3 rounds?
- Can we survive n rounds for every n? -> a finite number of rounds 
- Can the Duplicator survive for ever?

==Turn 1===
The spoiler chooses one element in $S$:
![[Playingfield Ehrenfeucht Fraisse_7.png|700]]
 And the Duplicator has plenty of choice and responds:
![[Playingfield Ehrenfeucht Fraisse_8.png|700]]

==Turn 2== 
The spoiler chooses to adjacent elements in $S$
![[Selection_134.png|700]]

The duplicator chooses another element in $S'$.
![[Selection_135.png|700]]

==Turn 3==
Now the spoiler chooses a node not in $S$ but in $S'$ he can also do that between the two elements that the Duplicator choose. This is possible due to the nature of $\mathbb{R}$ where there are always an infinite amount of elements between two elements. And with this he caught the Duplicator in a trap.
![[Selection_136.png|700]]

The duplicator can not choose a element between the previous chosen two elements of the Spoiler and hereby he loses.

<mark style="background: #FF5582A6;">Spoiler</mark> has a strategy to kill the <mark style="background: #014E11F2;">duplicator</mark> in the third rounds! They are only [[n-equivalence|2-equivalent]]

#### 2.3.2.1 How does this Example look in mathematical writing?

$$(\mathbb{R},<) \models \phi= \forall x \forall y \exists(x<y \to (x < z \land z < y))$$
$$(\mathbb{Z} \not \models \phi)$$ 

Question: How does this translate to [[n-equivalence]] Does it mean that the above formula can be at most [[n-equivalence|3-equivalent]] because it has only three nested Quantifiers?

## 2.4 When does the Spoiler always win?
On [[isomorphic|non-isomorpic]] finite structures, Spoiler wins  the Ehrenfeucht Fraise game eventually.

==Why? ==
Due to the __finite__ amount of elements in the structure at some point all elements of one of the two structures will be selected. Then, due to its [[isomorphic|non-isomorphic]] nature a ==element that is not present in one of the two structures will be chosen==.  In that moment the <mark style="background: #FF5582A6;">Spoiler</mark> wins as the <mark style="background: #014E11F2;">Duplicator</mark> can not chose the element as it is not present.

> [!note] A measure of similarity [[remoteness]]
> How long the duplicator survies in the game is a measure of how simmilar two structures are. The longer he survives the more simmilar the structures are.
> 
