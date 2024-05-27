The 28 a can be found in the note: [Verification 27](Verification%2027.md)

# 1 Star-free and first order definable languages

There are three kinds of [Regular Expression](Regular%20Expression.md)
- [General Regular Expressions](General%20Regular%20Expressions.md)
- [Restricted Regular Expression](Restricted%20Regular%20Expression.md)
- [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md)

We want to answer the question: ==What expressiveness do [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md) have?==

# 2 The main issue
We know that [Restricted Regular Expression](Restricted%20Regular%20Expression.md) (and [General](General%20Regular%20Expressions.md) ones) are as expressive as regular languages, and, similarly, ω-regular expressions are as expressive as ω-regular languages.

What about star-free regular expressions?

We are going to prove that they are as expressive as the first-order fragment of [S1S](Monadic%20second%20order%20of%20one%20sucessor.md), where quantification is restricted to first-order variables (positions in sequences).

What does this mean: The `*` gives the ability of second order logic. As the [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md) do not have the [Kleene star](Kleene-closure.md) it can not use the power of second order logic.

# 3 The infinite case
An analogous result holds for star-free and first-order ω-languages.

As we will see, they are also as expressive as the propositional temporal logic of linear time.

For the sake of simplicity, we restrict ourselves to the finite case.


>[!Note] [[Theorem 21]]
>Let $A$ be a finite alphabet. A language $W \subseteq A^*$ is star-free if and only if $(\iff)$ it is first order definable in [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) (with the ordering relation $<$ and unary predicates $Q_A$ for all $a \in A$)

==REMARK== While $+1$ is first-order definable in terms of $<$, the opposite is not, that is, $<$ i second-order, but not first order definable in terms of $+1$
$$< \xrightarrow{first-order} +1$$
$$+1 \not\xrightarrow{first-order} <$$

Hence, [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md)  with the ordering relation < and unary predicates $Q_A$, for all $a \in A$, is strictly more expressive than [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) with the successor function +1 and unary predicates $Q_a$ , for all $a \in A$.

## 3.1 Proof

### 3.1.1 First direction: [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md) $\rightarrow$ [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md)
The [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md) $\rightarrow$ [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) is straight forward.

It exploits the close correspondence between the operators $\cup,\sim,$ and $\cdot$ and the connectives $\neg,\lor$ and $\exists$, respectively.

Example:
$$\neg \emptyset \cdot(a\cup c)\cdot \sim (\neg \emptyset  \cdot b \cdot \neg \emptyset )$$

What does this mean:
1. $\neg \emptyset$  there needs to be some letters from the universe.
2. $a \cup c$ then follows a $a$ or a $c$
3. ~ complement
4. $\sim(\neg \emptyset  \cdot b \cdot \neg \emptyset)$ No b should occur after the steps 1.,2.,3. ($(\neg \emptyset  \cdot b \cdot \neg \emptyset )$ would mean there needs to be something then a $b$ then again something)  

over the alphabet $A={a,b,c}$ the same statement is defined by  the first order sentence:

$$\exists x ((x\in Q_{a}\lor x\in Q_{c})\land \neg \exists y(x\lt y\land y\in Q_{b}))$$

Therefore we can show that we can translate all signs from [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md) into [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md).

>[!Note] Why is there a * in a star free expression?
>
>It represents the universe and could also be expressed as $\neg \emptyset$. What is not allowed is for instance $ab^*$



The proof is by induction on the structure of the star-free expression.

Example:
We have  $U$ and $V$ which are the two first order formulas $\phi$ and $\psi$. Then the concatination of $U$ and $V$ i.e. $U \cdot V$ is can be expressed as the following:
$$U\cdot V=\exists x{\bigl(}\phi^{\prime}(x)\land\psi^{\prime}(x){\bigr)}$$

What are $\phi'$ and $\psi'$? This are relativizations regarding the position of $x$.
- $\phi'$ is only valid till x i.e. $<x$
- $\psi'$ is only valid after x i.e. $x<$


Now we have to show the other direction
### 3.1.2 Second direction: [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) $\rightarrow$ [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md)

The proof is by induction on the quantifier depth of formulas (and definitely less straightforward).

We focus on the most interesting and difficult case of the inductive step: the **existential quantifier.**

We consider the formula $\exists x \phi(x)$ of quantifier depth $n+1$ assuming (inductive hypothesis) that sentences of quantifier depth n define star-free languages. (The general case of formulas $\exists x \phi(x,\vec{y})$, with free variables $\vec{y}$ , is technically more involved.)

Lets look at the **proof idea**:
We rewrite the formula $\exists x \phi(x)$ into formulas of the form:


$$\exists x(\phi_{<x} \land x \in Q_a \land \phi_{>x})$$
Where $\phi_{<x}$ is the same as $\phi'$ described above, it only refers to the positions before $x$.

If $\phi_{<x}$ and $\phi_{>x}$ are of quantifier depth $n$, then such a formula describes a language:
$$U \cdot a \cdot V$$
where $U$ and $V$ are star free by induction hypotheses.


### 3.1.3 n-equivalence and (n,1)-equivalence relations

We introduce two fundametal relations:
- $\equiv_n$ [n-equivalence](n-equivalence.md) (as known form [V&V 7](Verification%207.md))
	The equivalence relation $\equiv_n$ over $A^*$ is defined as follows for all $u,v \in A^*$
	$u \equiv_n v$ if and only if $u$ and $v$ satisfy the same sentences of quantifier depth n
- $\equiv_{(n,1)}$ [(n,1)-equivalence](n-equivalence.md)
	The equivalence relation $\equiv_{(n,1)}$ over $A^* \times \mathbb{N}$ is defined as follows: for all $u,v \in A^*$ and $r,s \in \mathbb{N}$:
	$(u,r)\equiv_{(n,1)}(v,s)$ if and only if $(u,r)$ and $(v,s)$ satisfy the same formulas $\phi(x)$ of quantifier depth $n$

To deal with formulas with free variables (one in our case) we consider words with one distinguished position, that is, pairs $(u,r)$ with $u \in A^*$ and $1 \le r \le |u|$

### 3.1.4 Basic results
**FACT 1**:
For any $n \ge 1$ both $\equiv_{(n)}$ and $\equiv_{(n,1)}$ are [finite index](finite%20index.md), that is they have finitely many equivalence classes of $\equiv_{(n)}$ and $\equiv_{(n,1)}$.

**FACT 2**:
For any $n \ge 1$ , any class $W$ of words $u$ of $\equiv_{(n)}$ (resp. any class $\underline{W}$ of word models $(u,r)$ of $\equiv_{(n,1)}$) can be defined by a sentence $\phi_W$ (resp. a formula $\phi_{\underline{W}}$) of quantifier depth n.

Both facts can be proven by induction on the quantifier depth n.

The next proposition easily follows:

**Proposition 1**:
Any formula $\phi(x)$ of quantifier depth n is equivalent to a finite disjunction of formulas $\phi_{\underline{W}}$ (those formulas $\phi_{\underline{W}}$ such that $\underline{W}$ contains some $(u,r)$ satisfying $\phi(x)$)

How is this usefull:
We have a limited set of [Equivalence classes](Equivalence%20class.md). We can represent the formula $\phi(x)$ by a disjunction of formulas from the [Equivalence classes](Equivalence%20class.md). We use the [Hintikka Formula](Hintikka%20Formula.md) from each, if it fits it is part of the disjunction, if it does not the formulas of the equivalence class are not part of the disjunction.  Hereby we can find a different representation of a formula, by different formulas of some of the equivalence classes.

**Proposition 2:**
$\equiv_n$  and $\equiv_{(n,1)}$ relations are [Congruences](Congruence.md). That means:
- if $u \equiv_n v$ and $u' \equiv_n v'$ then $uu' \equiv_n vv'$
- if $u \equiv_n v$,$a\in A$ and $u' \equiv_n v'$ then $(uau';,|u|+1) \equiv_{(n,1)} (vav',|v|+1)$

Proposition two can easily be proven by exploiting the [Ehrenfeucht-Fraise game](Ehrenfeucht-Fraise%20game.md) game theoretic characterization of $\equiv_n$ and $\equiv_{(n,1)}$.

_Remark 1_:  Unlike Proposition 1, Proposition 2 depends on the  signature of [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) (binary ordering relation and unary predicates only)

_Remark 2_: The validity of  Proposition 2 is not restricted to finite words: it holds for any linear order expanded by unary predicates

Now we try all of this on paper:

>[!Reminder:]
>There is a correspondences between $u \equiv_n v$ and existence of a winning strategy for the duplicator in a game of $n$ rounds on the structures of $u$,$v$.

Now we will proof using the [Ehrenfeucht-Fraise game](Ehrenfeucht-Fraise%20game.md) the following feature of the [Congruence](Congruence.md):

 If $u \equiv_n v$,$a\in A$ and $u' \equiv_n v'$ then :
$$(uau',|u|+1) \equiv_{(n,1)} (vav',|v|+1)$$


Lets consider the case of $u \equiv_n v$:

How can we visually show the notion that the <mark style="background: #014E11F2;">duplicator</mark> has a winning game:

![](Verification%2028_image_1.png)

$S_x \rightarrow$ the choice of the <mark style="background: #FF5582A6;">Spoiler</mark> in the $x$th turn
$D_x \rightarrow$ the choice of the <mark style="background: #014E11F2;">duplicator</mark> in the $x$th turn

What is the rationale of the Duplicator in round 2:
He has two constraints:
1. he needs to choose a $c$
2. the $c$ needs to be left of the $b$ chosen by the spoiler in turn 1.

The Duplicator can play for $n$ rounds if $u \equiv_n v$ (has a winning strategy) 

The same holds true for $u' \equiv v'$ ( we just do not want to paint the image again)

Lets now consider the the strategy for the <mark style="background: #014E11F2;">duplicator</mark> in the game $\equiv_{(n,1)}$.

![](Verification%2028_image_2.png)

The nice thing here is that we have every time two structure $(u,u'\text{ and } v,v')$ as we have shown above, in the simple case we have a winning strategy in the individual substructures i.e. if there would only be $u$ we can apply the same winning strategy as above, if there was only $v$ we could apply the winning strategy from above.

This means that we can build a winning strategy also in the $\equiv_{(n,1)}$ case. We play four games at the same time, $u,v,u',v'$. If the spoiler plays in one of the substructures we respond in the winning strategy explained above, only relating the the state of the substructure that the spoiler has choosen i.e. the spoiler chooses $u$ then the duplicator chooses $u$ and so on.

 The problem is that there is also a binary relation (there is a relation between elements of $u,u'$ and $v,v'$), but luckily the ordering relation is true for free when we play in the same structure.


==Start VV29B==

Lets finish the proof now:

## 3.2 From the formula to the star-free expression

As a prelimnary step we observe that, in order to find the star-free counterpart of the formula $\exists x \phi(x)$ (of quantifier depth $n+1$) we can restrict our attention to the formula $\exists x \phi_{\underline{W}}(x)$

$$\exists x\phi(x)\leftrightarrow\exists x\bigvee_{\underline{W}}\phi_{\underline{W}}(x)\leftrightarrow\bigvee_{\underline{W}}\exists x \phi_{W}(x)$$

What we see here is the application of ==Proposition 1==: $\exists x\bigvee_{\underline{W}} \phi_{\underline{W}}(x)$ is the representation of $\exists x\phi(x)$ using the above described [Hintikka Formulas](Hintikka%20Formula.md) defined through the equivalence classes of $\equiv_n$.

Now we use a basic result of logic. If we have a quantification  infront of a disjunction we can exchange quantifier and disjunction (move it in).

Let us now consider a tripplet $(U,a,V)$ with $U,V$ beeing $\equiv_{n}$ classes and $a$ being a symbol of the [Alphabet](Alphabet.md) $A$ i.e.  $a \in A$.

As we have a finite set of equivalence classes as $\equiv_n$ is [finite index](finite%20index.md) (**FACT 1**) and we have a finite alphabet $A$, we have a finite set of tripples.

If there exists $u_0 \in U$ amd $v_0 \in V$  such that $(u_0 a v_0,|u_0|+1) \in \underline{W}$, then by [Proposition 2](Proposition%202.md), it holds that  $(u a v,|u|+1) \in \underline{W}$ for all $u \in U$ and $v \in V$.

This allows us to conclude that all words in $U \cdot V$ satisfy $\exists x\phi(x)$. 

Hence $\exists x \phi_{W}(x)$ defines (can be mapped into the) the (finite) union of the sets/languages $U \cdot a \cdot V$ , selected from all tripplets $(U,a,V)$ such that $U,V$ are $\equiv_n$ classes that contain elements $u_0,v_0$ as described above.

Since by the inductive hypothesis, $U,V$ are star-free sets/languages, it immediately follows that $\exists x \phi_{W}(x)$ defines star-free languages.


The relationships between star-free expressions and formulas of the first-order fragment of S1SA is tighter than expressed in McNaughton-Papert theorem.

It is indeed possible to show that the classification of star-free regular languages by **dot-depth**, that is, the number of alternations between concatenation and Boolean operations in the expressions that define them ==coincide== with the classification of languages definable in the first-order fragment of [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) in terms of **quantifier alternation depth**.



>[!note] [[Theorem 22]]
>Let $A$ be a finite alphabet. An $\omega \text{-language}$ $L \subseteq A^{\omega}$ is first order definable in [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) if and only if  $L$ is obtained from $A^{\omega}$ by repeated application of Boolean operations and concatenations with star-free sets/languages $W \subseteq A^*$ on the left


$\omega \text{-languages}$ that satisfy the above condition of [Theorem 22](Theorem%2022.md) are called star-free $\omega \text{-languages}$.


Ladner showed that star free $\omega \text{-languages}$  are a proper subclass of $\omega \text{-languages}$.


