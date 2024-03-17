# 1 [Determinization](Determinization.md)


## 1.1 Exercise
Let $A=\{a,b\}$ and let $L=\{ \alpha \in A^\omega: \exists \overset{<\omega}{n} \quad \alpha(n) =a\}$
In words there should be less than infitnite positions ($<\omega$) $n$ that have the value $a$. i.e. All words that have a finite number of $a$.

Build a [NBA](Buechi%20automata.md) that recognizes this language:

![](Verification%2027_image_1.png)

Now we show that a [DBA](Buechi%20automata.md) can not recognize a language like this, with the result that a [NBA](Buechi%20automata.md) is more powerful than [DBA](Buechi%20automata.md)s.

We exploit the previous proposition namely:
The characterization of the Languages recognized by the [DBA](Buechi%20automata.md) have a [Vectorial closure](Vectorial%20closure.md) for some language $\omega$ i.e. $\overrightarrow{w}$.


By contradiction let us assume that $L$ can be expressed as $\overrightarrow{w}$ i.e. $L=\overrightarrow{w}$ for some language $w \in A^*$ (regular).

Since $b^\omega \in L (= \overrightarrow{w})$ it follows that there exists $n_1$ such that $b^{n_1} \in \mathbb{N}$ i.e. there are infinitely many prefixes in $b^\omega$ and we choose one, namely $n_1$.

Now, since $b^{n_1}ab^\omega \in L (= \overrightarrow{w})$ i.e. belongs to the language (the word only ends in $b$s), there exists $n_2$ such that $b^{n_1}ab^{n_2} \in w$. Now since $b^{n_1}ab^{n_2}ab^{n^3} \in L$ there exists $b^{n_3}$ such that  $b^{n_1}ab^{n_2}ab^{n^3} \in w$ etc....

By repeating this step infinitely many times I can obtain a $w-\text{word}$ of the form $b^{n_1}ab^{n_2}ab^{n^3}...$ that has infinitely many prefixes belonging to $\omega$ but does not belong to $L$  (because it has infinitely many occurrences of the symbol $a$)
$\square$

Exercise:
Now we try to build a automaton that accepts the Language that is the complement of the language before.
Let $A=\{a,b\}$ and let $\overline{L}=\{ \alpha \in A^\omega : \exists^{\omega} n \quad \alpha(n)=a\}$ 
i.e. a language that has infinitely many $a$s. Build a [DBA](Buechi%20automata.md) that recognizes $\overline{L}$.

 ![](Verification%2027_image_2.png)

But this is is a [DBA](Buechi%20automata.md) (it has one case for each letter)!

This means that we have a language $L$ that is only acceptable by [NBA](Buechi%20automata.md) but its complement i.e. $\overline{L}$ can be accepted by a less expressive [DBA](Buechi%20automata.md)! From here follows that [DBA](Buechi%20automata.md)s are not closed under [Complementation](Complementation.md).

As we found a language that can be expressed by a [DBA](Buechi%20automata.md) but its complement becomes only expressable by a [NBA](Buechi%20automata.md).

>[!note] 
>[Deterministic Buechi Automata](Buechi%20automata.md) are not closed to [Complementation](Complementation.md)

![](Verification%2027_image_3.png)


Thats shit. So we try to find automata that are actually closed to [Complementation](Complementation.md), as complementation as the computation costs for complementation is so low and we want to do it regularly.

Therefore people came up with [[Muller Automata]].

# 2 [Muller Automata](Muller%20Automata.md)

[Muller Automata](Muller%20Automata.md) are different from [Buechi automata](Buechi%20automata.md) by their acceptance condition. The [Muller Automata](Muller%20Automata.md) demands a higher control of the computation and is ==more strict== than with [Buechi automata](Buechi%20automata.md).

>[!Definition] Muller Automata
>A [DMA](Muller%20Automata.md) is a tuple:
>$$\mathcal{A}=(Q,A,\delta,q_0,\mathcal{F})$$
>- $Q$ the set of states
>- $A$ the alphabet
>- $\delta$ (determinisitic) transition functions
>- $q_0$ initial state
>- $\mathcal{F}$
>$Q,A$ and $q_0$ are defined as for the [DBA](Buechi%20automata.md)
>$\mathcal{F}$ is a subset of the powerset of $Q$
>i.e. $\mathcal{F}\subseteq 2^Q$ i.e. a set of subsets of $Q$
>
>The computation $\sigma$ of $\mathcal{A}$ on an $\omega\text{-word}$ $\alpha$ is successfull if and only if ($\iff$) $IN(\sigma)$ belongs to $\mathcal{F}$ i.e. $IN(\sigma)\in \mathcal{F}$.
>
>$\mathcal{A}$ accepts $\alpha$  if the computation $\sigma$ of $\mathcal{A}$ on $\alpha$ is successful.
>The language $L(\mathcal{A})$ is the set of all and only those $\omega\text{-words } \alpha$ accepted by $\mathcal{A}$. 

By that we do not only define which states do occur infinitely many times but also which states should not occur infinitely many times.

==Exercise==

It is easy to show that every [DBA](Buechi%20automata.md) is equivalent to a [DMA](Muller%20Automata.md). Whenever there is a [DBA](Buechi%20automata.md) I can build a [DMA](Muller%20Automata.md) that recognizes the same Language.

Let $\mathcal{A}$ be the [DBA](Buechi%20automata.md) $(Q,A,\delta,q_0,F)$. Build an equivalent [DMA](Muller%20Automata.md).

We only need to turn [DBA](Buechi%20automata.md) $F$ into $\mathcal{F}$ of the [DMA](Muller%20Automata.md).

Where $\mathcal{F}=\{P \in 2^Q: P \cap F \neq  \emptyset \}$
($P$ is a subset of $Q$)
We only put in the states that occur infinitely many times. All others do not matter. With [DBA](Buechi%20automata.md) only one of the final states needs to occur infinitely many times. With the [DMA](Muller%20Automata.md) all states in $\mathcal{F}$ need to occur infinitely many times i.e. we put in all states of $F$ that occur infinitely many times and leave the states that do not occur infinitely many times.

---

27 b
 
---

Exercise:

lets Express the [DBA](Buechi%20automata.md) from before as a [DMA](Muller%20Automata.md):

![](Verification%2027_image_2.png)

We only need to adapt $F$ to $\mathcal{F}$.
$\mathcal{F}$ must contain all possible subsets of $F$ that contain a final state: 
$$\mathcal{F}=\{\{q_0\},\{q_0,q_1\}\}$$

>[!Note] 
> [Deterministic Buechi Automata](Buechi%20automata.md) are a subset of [Deterministic Muller Automata](Muller%20Automata.md) i.e.
> $$DBA \subseteq DMA$$

[NMA](Muller%20Automata.md) can be obtained from [DMA](Muller%20Automata.md) by replacing the [Function](Function.md) $\sigma$ by the [relation](Relationship.md) $\Delta$.

>[!Proposition] (Exercise)
>[NBA](Buechi%20automata.md) and [NMA](Muller%20Automata.md) have the same expressive power

==Proof==
($\rightarrow$) 
you proceed like in the deterministic case (one needs to define the $\mathcal{F}$)

($\leftarrow$) 
You pass through [S1S](Monadic%20second%20order%20of%20one%20sucessor.md). One takes a [NMA](Muller%20Automata.md) encodes it as [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) function and as we know [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) and [NBA](Buechi%20automata.md) are equivalent, and we know that [NBA](Buechi%20automata.md) and [NMA](Muller%20Automata.md) are equivalent .

$\phi$ of [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) of the form 
$$\exists ... \exists(\phi_1 \land \phi_2 \land \phi_3)$$
Where:
- $\phi_1$ general condition of the initial state (unchanged)
- $\phi_2$ [Rule of Consequentiality](Rule%20of%20Consequentiality.md) (unchanged)
- $\phi_3$ Acceptance condition must be adapted
	How do we encode the acceptance condition in a [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula
	We need to constraint the subset of states to occur infinitely many times. And the complement of states to occur a finite many times.



# 3 Summary

[DBA](Buechi%20automata.md) $\subset$ [NBA](Buechi%20automata.md)
[NBA](Buechi%20automata.md) $\equiv$ [NMA](Muller%20Automata.md)
[DBA](Buechi%20automata.md) $\subseteq$ [DMA](Muller%20Automata.md)
[DMA](Muller%20Automata.md) $\subseteq$ [NMA](Muller%20Automata.md)

The goal is to show that [NMA](Muller%20Automata.md) and [DMA](Muller%20Automata.md) are equivalent, then it follows that [DBA](Buechi%20automata.md) has the same relation to [NBA](Buechi%20automata.md) as to [DMA](Muller%20Automata.md) following that [DBA](Buechi%20automata.md) is a proper subset of [DMA](Muller%20Automata.md) i.e. ([DBA](Buechi%20automata.md) $\subset$ [DMA](Muller%20Automata.md)) (see the image below):

![](Verification%2027_image_4.png)

To grab ahead: 
>[!note]
>[NBA](Buechi%20automata.md) $\equiv$ [DMA](Muller%20Automata.md)

# 4 Now to some results without proofs

>[!note] [[Theorem 18]]
>[Deterministic Muller Automata](Muller%20Automata.md) are closed under Boolean operations i.e. ($\cup,\cap,\overline{}$) i.e. And, or and [Complementation](Complementation.md)


>[!note] [[Lemma 14]] 
>An $\omega \text{-language } L \subseteq A^\omega$ is recognized by a [DMA](Muller%20Automata.md) if and only if ($\iff$) $L$ is a boolean combination (on $A^{\omega}$) of Languages of the form $\overrightarrow{w}$ where $w$ is a regular language.

Reasoning:  
If $w$ is a regular language the vectorial closure is recognized by a [DBA](Buechi%20automata.md). If it is recognized by a [DBA](Buechi%20automata.md) we know that it is also recognized by a [DMA](Muller%20Automata.md). And the [Theorem 18](Theorem%2018.md) says that [DMA](Muller%20Automata.md) is closed under boolean operations. As [the closedness property](Closed%20Formulas.md) describes if one has multiple languages are accepted by a [DMA](Muller%20Automata.md) also the boolean combination of them is accepted.

>[!note] [[Lemma 15]] 
>Every $\omega\text{-language } L \subseteq A^\omega$ which is recognized by an [NBA](Buechi%20automata.md) can be expressed as a finite union of languages of the form $\overrightarrow{u} \cup \overline{\overrightarrow{v}}$ where $u,v, \subseteq A^*$ are regular languages.

Why is it so hard to prove [Lemma 15](Lemma%2015.md).

There are two difficult steps, the second one is more difficult than the first.

1. Problem
$u \cdot v^w=u \cdot \overrightarrow{v}$ under the assumption that $v\cdot v=v$ (if I take two word of $v$ and concatenate them I stay inside $v$ closedness under [Concatenation](Concatenation.md)). Even if $v$ is closed the initial statement ($u \cdot v^w=u \cdot \overrightarrow{v}$) is not true.

2. Problem
$u \cdot \overrightarrow{v} \neq \overrightarrow{u \cdot v}$. where $u,v$ are regular sets


Lets focus on the 1. Problem:
$u \cdot v^w=u \cdot \overrightarrow{v}$ with $v \cdot v=v$
We can replace $=$ with a double inclusion($\subseteq,\supseteq$) and one of the two inclusions is actually ==true==, which is:
$$u \cdot v^w \subseteq u \cdot \overrightarrow{v}$$

![](Verification%2027_image_5.png)

As $v$ has an infinite number of prefixes in itself it has the [Vectorial closure](Vectorial%20closure.md).
thus we can also assume that: $\alpha \in u \cdot \overrightarrow{v}$  

But we also need to show $\supseteq$ which is unfortunately not true...

We will show not that $\supseteq$ is not true, by giving a counterexample. In this case that $u \cdot \overrightarrow{v} \not \subseteq u \cdot v^\omega$.

Let $v=(ab^*)^*$ and $u =\{\epsilon\}$

To clarify $v$ we give some examples
- $ab^*$ is for instance $abbbb$ or $abb$
- $(ab^*)^*$ is for instance $abbbbabb$ or $abababb$
special cases are the empty word $\epsilon$ or a set of $a$s with zero $b$s for instance $aaa$.

It is easy to see that for this language $v\cdot v=v$.
By concatenating $abbbbabb$ or $abababb$ which are part of $v$ we get $abbbbabbabababb$ which is also in $v$ which is also the requirement shown above.

Let us provide a $\omega \text{-word}$ $\alpha$ such that $\alpha \in u \cdot \overrightarrow{v}$ but $\alpha$ does not belong to $u \cdot v^\omega$ i.e. $\alpha \not \in u \cdot v^\omega$.

Let $\alpha$ be $a\cdot b^w$. Does $a \cdot b^\omega \in \overrightarrow{v}$. Yes it does because the prefixes of $\alpha$ for instance $abbb$ are actually extisting in $v$. This is because of the creation of $v$. If we look at the inner part of $v$ i.e. $ab^*$ it is the same as the definition of alpha.  visually this means:

![](Verification%2027_image_6.png)

==All prefixes of $\alpha$ belong to the vectorial closure of $v$.

Now does $\alpha$ also belong to $u \cdot v^\omega$? ==No==

![](Verification%2027_image_7.png)

$v^\omega$ is a infinite concatenation of $v$s i.e.
$vvvvvvvv$ which is actually part of $v$ by the condition before i.e. $v \cdot v =v$

But $\alpha$ consists of one occurrence of $v$ but then the rest of the word is not part of $v$ i.e. $\alpha=v \cdot bbbbb...$ and $bbbb\dots b \not \in v$.

This does not show that the lemma above is not true, but that it is rather ==complicated== to prove it.

The ==essence== of this exercise is that if we have a language defined as $u \cdot v^\omega$ and we want to define the same language using [Vectorial closure](Vectorial%20closure.md) i.e. $u \cdot v_1^\omega$. $v$ and $v_1$ can not be the same languages.

To problem *2.*
$u \cdot \overrightarrow{v} \neq \overrightarrow{u \cdot v}$. where $u,v$ are regular sets.
Therefore we do the same trick expressing $=$m as $\subseteq$ and $\supseteq$.

In one direction is indeed again the case:
$u\cdot \overrightarrow{v} \subseteq \overrightarrow{u \cdot v}$

$\alpha \in u \cdot \overrightarrow{v}$

![](Verification%2027_image_8.png)

it is immediate to see that $\alpha$ also belongs to $\overrightarrow{u \cdot v}$.
When we take the same u from the image above, we can also concatenate the three different length $v$ and can represent the same words as above, meaning that they also belong to $\overrightarrow{u \cdot v}$.

 ![](Verification%2027_image_9.png)

Now lets look at $\supseteq$ i.e. $\overrightarrow{u\cdot v} \supseteq u \cdot \overrightarrow{v}$ .

What is the difference: in $u \cdot \overrightarrow{v}$ when switching from one prefix of $v$ to another prefix of $v$ $u$ always needs to stay the same. In $\overrightarrow{u\cdot v}$ we can change $u$ meaning as in the image above hinted that $u$ can be different words i.e. $u_1,u_2,u_3$

Disproving this is simple we need a counterexample where we actually need to change the $u$ component.

==Counterexample==
$u=b^*$ and $v=b$

And let us consider the $\omega\text{-word}$ $\alpha  =b^\omega$.

First we see that $\alpha \in \overrightarrow{u \cdot v}$

![](Verification%2027_image_10.png)
Then we learn that $\alpha \not \in u \cdot \overrightarrow{v}$.

![](Verification%2027_image_11.png)

This is because when we take a word $u$ it is easy to find for instance $b^7$ (as in the example above) but when we want to find infinitely many  prefixes in the word $\alpha$ this is not possible as $v$ only has one single element i.e. $b$ that means for every word $u$ we only have one prefix, which is not ==infinitely many== showing that indeed $\alpha = b^* \not \in u \cdot \overrightarrow{v}$.


The ==essence== of this exercise is that if we have a language defined as $u \cdot v^\omega$ and we want to define the same language using [Vectorial closure](Vectorial%20closure.md) i.e. $u \cdot v_1^\omega$. $v$ and $v_1$ can not be the same languages.

When looking at this as a quantifier we see the difference better:
$$u \cdot \overrightarrow{v} \rightsquigarrow \exists u\forall^\omega v \dots$$
$$\overrightarrow{u \cdot v} \rightsquigarrow \forall^\omega \text{prefixes} \quad \exists u\text{-component}$$
i.e. for each choice of the prefix we can choose a distinct $u\text{-component}$. ==This is related to the order of quantifiers==.

We can not switch in general the quantifier order, i.e. $\forall \exists$ t $\exists \forall$


>[!Theorem] [Theorem 19](Theorem%2019.md) 
>An $\omega\text{-language}$ is $\omega\text{-regular}$  (that is recognizable by an [NBA](Buechi%20automata.md)) if and only if ($\iff$) if it is recognizable by a [DMA](Muller%20Automata.md).

Advantages: We can easily create a complement Language.

Proof [Theorem 19](Theorem%2019.md).
([NBA](Buechi%20automata.md) $\rightarrow$ [DMA](Muller%20Automata.md) )
This follows from [Lemma 15](Lemma%2015.md) (Characterization of $\omega\text{-regular}$ languages as finite unions of objects of the form $\overrightarrow{u} \cup \overline{\overrightarrow{v}}$ ) and the previous one [Lemma 14](Lemma%2014.md) (a Müller recognizable language can be expressed as a Boolean combination of regular sets i.e. of Languages of the form $\overrightarrow{w}$ where $w$ is a regular language.).

[Lemma 15](Lemma%2015.md) allows us to express a regular language with set of the form $\overrightarrow{u} \cup \overline{\overrightarrow{v}}$.

[Lemma 14](Lemma%2014.md) says whenever one has a language defined in this way (a boolean combination (for instance the [Union](Union.md), in our case $\overrightarrow{u} \cup \overline{\overrightarrow{v}}$.) one can find a [DMA](Muller%20Automata.md)

([DMA](Muller%20Automata.md) $\rightarrow$ [NBA](Buechi%20automata.md))
We can use again [Lemma 14](Lemma%2014.md). We start again by the characterization of languages recognized by [DMA](Muller%20Automata.md) as a Boolean combination of regular sets i.e. of Languages of the form $\overrightarrow{w}$ where $w$ is a regular language.

Then we remember that languages of the form $\overrightarrow{u}$ for $u$ being regular, are recognized by [DBA](Buechi%20automata.md) and we exploit the closure of [NBA](Buechi%20automata.md) with respect to $\cup,\cap$ and $\overline{}$ (the complement). $\square$

# 5 The relationship between [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) and [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md)
>[!Theorem] [[Theorem 20]]: the expressiveness of [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md).
>An $\omega\text{-language}$ $L \subseteq A^\omega$ is  $\omega\text{-regular}$ (definable in [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)) if and only if ($\iff$) $L$ is definable in [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md) meaning that ==[S1S](Monadic%20second%20order%20of%20one%20sucessor.md) and [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md) are equally [expressive](expressiveness)==

Proof:
([S1S](Monadic%20second%20order%20of%20one%20sucessor.md) $\rightarrow$ [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md)):
We showed already that it is easy to constraint [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) to finite sets.

([WS1S](Monadic%20second%20order%20of%20one%20sucessor.md) $\rightarrow$ [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)):
Let us assume that $L \subseteq A^\omega$ is $\omega\text{-regular}$. By [Mc Naughtons Theorem](Theorem%2019.md), we know that $L$ can be expressed as a Boolean combination of languages of the form $\overrightarrow{w}$, with $\omega$ being regular.
We show now how to characterize languages of the form $\overrightarrow{w}$, with $\omega$ being regular, with a formular of [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md).

By the result about [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) and [Finite State Automata](Finite%20State%20Automata.md), we know that there exists an [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula $\phi(X_1,X_2,...,X_n)$ that defines the regular language $w$ accepted by a [FSA](Finite%20State%20Automata.md).

It is possible to build a formula,$\psi(X_1,X_2,\dots,X_n,y)$ of [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md) that when interpreted by $\omega\text{-words}$, constrains the prefix of such an infinite word up to position $y$ to satisfy $\phi(X_1,X_2,...,X_n)$.

To this end it suffices to relativize second order quantification up to $y$.

Examples:
1.  $\exists X(0 \in X) \quad \overrightarrow{relativized} \quad \exists X (\forall x(x \in X \rightarrow x < y ) \land 0 \in X)$  
2. $\forall X(0 \in X) \quad \overrightarrow{relativized} \quad \exists X (\forall x(x \in X \rightarrow x < y ) \to 0 \in X)$  

Since the original formula $\phi(X_1,X_2,\dots,X_n)$ defines the language $w$, the [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula that defines $\overrightarrow{w}$ is the following one:
$\forall x \exists y(x<y \land (\psi(X_1,X_2,\dots,X_n)))$

# 6 Summarizing we have this relations:

![](Verification%2027_image_12.png)
