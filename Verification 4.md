Info: Video 4a,4b

Model checking in [[QBF]]

```python
def Model-check(phi,S):
	#### same as in propositional logic 
	if phi = p:
		return S(p)
	elif phi = phi_1 or phi_2:
		return Model-check(phi_1,S) 
				or Model-check(phi_2,s)
	elif phi = phi_1 and phi_2:
		return Model-check(phi_1,S) 
				and Model-check(phi_2,s)
	elif ...
 	####
	elif phi = \exists p phi':
		return Model-check(phi',S[p:= True]) 
			or Model-check(phi',S[p:=False])
	elif phi = \forall p phi':
		return Model-check(phi',S[p:= True]) 
			or Model-check(phi',S[p:=False])

 ```

The new added parts are setting the variable $p$ to the wanted value and with the $\exists$ one of the two Model-checks need to be True with the $\forall$ both of the Model-checks need to be True. $\texttt{phi'}$ denotes in the algorithm the part of the formula that is behind the $\exists$ and the $\forall$.

The <mark style="background: #014E11F2;">time complexity</mark> is exponential as we have two recursive calls each $\exists$ or $\forall$. i.e. $O(|\phi|^{q\cdot d(\phi)})$ where $q$ is the number of quantifiers, and $d(\phi)$ is the quantifier depth.

```ad-note 
what is the quantifier depth?
The number of consecutive quantifiers
$\exists p  \forall q \forall r$ would have the quantifier depth 3
```

Complexity: __PSPACE__-complete 

# [[Satisfiability]] in [[QBF]]
Reduces the model-checking for [[QBF]]
[[QBF]] -> $\phi(p_1,p_2..)$ satisfiable $\iff$ $\exists p_1 \exists p_2... \phi$ holds over empty structure.

What does this mean:
We can rewrite every [[Satisfiability]] problem of every formula $\phi$ into another formula $\phi'$ using the $\exists$ quantifier. Then we apply the model-checking on this new formula $\phi'$. If there exists a solution to the formula the entire thing is satisfiable.i

This is caused by the meaning of the $\exists$ quantifier. 	$\exists$ asks is there one mapping onto either true or false i.e. is it satisfiable?

Complexity: __PSPACE__-complete

Now we look at the difference of the satisfiability tree in [[QBF]] and [[SAT]] (propositional logic)

Just has one path as there are only $\exists$ when looking at satisfiability
![[Satisfiability_SAT.png|300]]

Has multiple paths as there are $\exists$ as well as $\forall$ which split up the tree
![[Tree_satisfiability_QBF.png|300]]

```ad-note
title: [[lemma 5]]
In [[QBF]] every formula is equivalent to one in [[Prenex Normal Form]] which can be computed efficiently
```

Example:
Not in [[Prenex Normal Form]]:
$\phi=(\exists p \phi_1) \land \phi_2$

Push quantifiers outside by using [[Lemma 4 (renaming)]]:
$\exists p \phi_1 \lor \phi_2$ is rewritten into $\exists q (\phi_1[p/q]) \lor \phi2$
$\exists p \phi_1 \land \phi_2$ is rewritten into $\exists q (\phi_1[p/q]) \land \phi2$
...

<mark style="background: #FF5582A6;">One has to take care!</mark> the condition is that p is not occuring free in $\phi_2$ otherwise we would change the meaning of the formula! Solution: one can rename the variable $p$ in $\exists p \phi_1$ to another name i.e. $u,l,k$ so that the variable does not occur freely in $\phi_2$.

```ad-note 
title: [[Lemma 6]]
Model-checking [[QBF]]'s in [[Prenex Normal Form]] with n quantifiers ($\exists,\forall$) has the time complexity:

$$\Sigma_n=NP^{coNP^{...}} \text{ or } \Pi_n=coNP^{NP^{...}}$$

Application: the sequence of NP and co-NP depends on which quantors one uses: i.e. $\exists p \forall q \exists r \phi$ would have the complexity class $NP^{co-NP^{NP}}$
```

What does $NP$ complexity mean:
The problem can be solved with a machine in a $\textit{non deterministic}$ in polynomial time.  When something is in the power i.e. $NP^{coNP}$ it means that the main process has a subprocess that solves $coNP$ problems

Application:
problem: does the device admit a run from initial to target state? Simmilar as in the class [[Verification 3]]

Consider a device whose internal state is encoded by $k$ bits $\underline{p}=p_1,...,p_n$
- initial state is described by a propositional formula $\phi_{init}(\underline{p})$
- target state is described by a propositional formula $\phi_{target}(\underline{p})$
- Transitional formulas are described by a propositional formula $\phi_{step}(\underline{p},\underline{p'})$

In [[Propositional Logic]] the solution went like this:
The formula describes it:

$$\phi_{reach}(\underline{p_1},....,\underline{p_n})=\phi_{init}(\underline{p_1}) \land \phi_{step} (\underline{p_1},\underline{p_2})\land \text{ ... } \land \phi_{step}(\underline{p_{n-2}},\underline{p_{n-1}}) \land \phi_{target}(\underline{p_n})$$

Now we sum up all $\phi_{step}$ to get from $\underline{p_{init}}$ to $\underline{p_{target}}$ as $\phi_{run}[p_{init},p_{target}]$.

In the next step we split the path up into two paths from $p_init$ to $p_r$ and from $p_r$ to $p_target$ with about equal length $\frac{n}{2}$. Then we split this sub-path again up recursively till the path is equal to $\phi_{step}[\underline{p_k},\underline{p_{k+1}}]$ where k is some step in the path. 
Mathematically written:
$$\phi_{run}^{n}(\underline{p},\underline{q})=\exists r (\phi_{run}^{n/2}(\underline{p},\underline{r})\land \phi_{run}^{n/2}(\underline{r},\underline{q}))$$
$$\phi_{run}^{n/2}(\underline{p},\underline{q})=\exists r (\phi_{run}^{n/4}(\underline{p},\underline{r})\land \phi_{run}^{n/4}(\underline{r},\underline{q}))$$
$$...$$
$$\phi_{run}^{1}(\underline{p},\underline{q})=\phi_{step[\underline{p},\underline{q}]}$$

The depth of this formulas is actually proportional to the number of bits $k$ i.e. $O(2^k)$. The size of the formula should be of exponential size as in [[Propositional Logic]]

What is the advantage? Complexity is similar? We can re-write:
$$\phi_{run}^{n}(\underline{p},\underline{q})=\exists \underline{r} \forall \underline{s} \forall \underline{t} ((\underline{s},\underline{t}=\underline{p},\underline{r} \implies \phi_{run}^{n/2}[\underline{p},\underline{r}])\land( \underline{s},\underline{t}=\underline{r},\underline{q} \implies\phi_{run}^{n/2}[\underline{r},\underline{q}]))$$
This makes that we have two times $\phi_{run}^{n/2}(\underline{r},\underline{q})$ that are equivalent and using Rules
$$(A \implies C) \land (B \implies C) \equiv (A \lor B) \implies C$$

We can rewrite again to:

$$\phi_{run}^{n}(\underline{p},\underline{q})=\exists \underline{r} \forall \underline{s} \forall \underline{t} ((\underline{s},\underline{t}=\underline{p},\underline{r})\lor( \underline{s},\underline{t}=\underline{r},\underline{q} )) \implies \phi_{run}^{n/2}[\underline{r},\underline{q}]$$

With the result that the algorithm is linear in $k$

When using quantifiers we can make formulas much more [[Succinctness|succinct]]. And one can exchange a huge conjunction $(\land)$ by a universal quantification

---

break

---

[[QBF]]
# [[FO - First order logic]]
<mark style="background: #014E11F2;">Vocabulary:</mark> 
- Boolean connectives $\land,\lor,\neg,\iff,\implies$
- $\forall,\exists$ Quantifiers
- Relationship symbols $\Sigma = {R,S,T}$ (= always in the signature)
- first order variables: $x,y,z$

<mark style="background: #014E11F2;">Syntax:</mark> 
$$\phi =|\phi \land \phi|\phi \lor \phi|\neg\phi| \phi \iff \phi|\phi \implies \phi|...|R(x_1...x_k)|...|\exists x \phi|\forall x \phi$$ 

<mark style="background: #014E11F2;">semantics</mark> :
A structure now consists of  a *universe* $U^s$ which is a set of objects
+ *interpretations* $R \implies R^S \subseteq U^S \times ... \times U^S$
								$x \implies x^S \in U^S$ 
What does this mean?
The first $R$ is the Relationship symbol. $R^S$ is the real Relationship
$x$ is a variable that is getting mapped on an object of the universe $x^s$.

$$S \models \phi_1 \lor \phi_2 \iff S \models \phi_1 or S \models \phi_2$$
$$S \models R(x_1,...,x_k) \iff (x_1^s,...,x_k^s) \in R^S$$
$$S \models \exists x \phi \iff S[x:=u] \models \phi \text{ for some } u \in U^s$$
$$S \models \forall x \phi \iff S[x:=u] \models \phi \text{ for every } u \in U^s$$

What is the link to [[QBF]]:
When you define the Universe $U^S$ as $U^S=\{\textit{true,false}\}$ [[FO - First order logic]] becomes (almost) [[QBF]]

Example for a relation: Database:

| movies       | year |
| ------------ | ---- |
| Bond         | 2020 |
| Harry Potter | 2010 |
| ...          | ...  | 
(Bond,2020) $\in R$ 
If we want to use such a tuple we write in a formula $R(x_1,x_2)$
while $x_1$ stands for the movie name and $x_2$ stands for the release year.

### Example 1:
If all <mark style="background: #014E11F2;">humans</mark> are <mark style="background: #FF5582A6;">mortal</mark> , and
<mark style="background: #ADCCFFA6;">Socrates</mark> is <mark style="background: #014E11F2;">human</mark> ,
then <mark style="background: #ADCCFFA6;">Socrates</mark> is <mark style="background: #FF5582A6;">mortal</mark> .

$\phi(y_0)=((\forall x A(x)\rightarrow B(x)) \wedge A(y_0)) \rightarrow B(y_0)$

Lets define what is the Universe and what the relation-symbols are
Socrates, Plato -> humans
Cyclop -> mythological figure that can also die (is killed by Ulisses in the Illias)
Jupyter -> god so not mortal


$$\begin{equation}
  S:
    \begin{cases}
      U^S & =\text{\{Socrates, Plato, Cyclop, Jupyter\}}\\
      A^S & =\text{\{Socrates, Plato\} -> humans}\\
      B^S & =\text{\{Socrates, Plato, Cyclop\}} \text{ -> Mortals}\\
      y_0^S & =\text{Socrates}
    \end{cases}       
\end{equation}
$$

We look at unary relations. That means that all relations are subsets of the universe $U^S$. The universe can not be empty.


### Example 2:
<mark style="background: #014E11F2;">There is a node</mark> in the graph
that is<mark style="background: #FF5582A6;"> isolated</mark> 
from <mark style="background: #ADCCFFA6;">all other nodes</mark> 

$$\phi()= \textcolor{green}{\exists x} \textcolor{blue}{\forall y} (\neg (x=y) \implies \textcolor{red}{\neg E}(x,y))$$

relationship symbols = {=,E}
free variables = {} -> all variables are part of Quantifiers
The 2 relations are binary relations

$$\begin{equation}
  S:
    \begin{cases}
      U^S & =\text{\{Nodes of a graph\}}\\
      E^s & =\text{\{edges of a graph\}}\\
	  =^S & = \{(x,x) | x \in U^S\}\text{ -> quality relation}
    \end{cases}       
\end{equation}
$$


1. $\neg (x=y)$ means y is different from x
2. $E(x,y)$ returns true if they have a edges that connect themselv 

### Example 3:
<mark style="background: #014E11F2;">There is a man</mark> such That
when he <mark style="background: #FF5582A6;">runs</mark> 
<mark style="background: #ADCCFFA6;">everybody</mark> <mark style="background: #FF5582A6;">runs</mark> 

$$\phi() = \textcolor{green}{\exists} x (\textcolor{red}{R}(x) \implies \textcolor{blue}{\forall y} \textcolor{red}{R}(y))
$$

2 variables -> none of them free
1 relation

$$\begin{equation}
  S:
    \begin{cases}
      U^S & =\text{\{Ben,Han,Leia,Luke\}}\\
      R^s & =\text{\{Ben, Han\}}\\
    \end{cases}       
\end{equation}
$$

Does the structure $S$ hold?

Yes because we have a $\exists$. It has to be only true for one of the elements of the universe:
- As Leia and Luke are not running it holds true. As they do not run they do not make everybody else run. i.e. the make everybody else run is not triggered i.e. the formula is true for Leia and Luke.
- If we choose Ben and Han the formula is false as Ben is running and while he runs only Han runs and vice-versa. Because Leia and Luke are not running the formula is false.
- If we exchange the $\exists x$ by $\forall x$ everybody needed to run when one of the elements run i.e. the formula could not be True as Leia and Luke never run.

What happens when we change the Structure:

$$\begin{equation}
  S':
    \begin{cases}
      U^S & =\text{\{Ben,Han,Leia,Luke\}}\\
      R^s & =\text{\{Ben, Han,Leia,Luke\}}\\
    \end{cases}       
\end{equation}
$$

Then the formula is true for both:
$$\phi() = \textcolor{green}{\exists} x (\textcolor{red}{R}(x) \implies \textcolor{blue}{\forall y} \textcolor{red}{R}(y))
$$
 and
 $$\phi() = \textcolor{green}{\forall} x (\textcolor{red}{R}(x) \implies \textcolor{blue}{\forall y} \textcolor{red}{R}(y))
$$

### Example 4:

R is a function

$\phi = \forall x \exists y R(x,y) \land (\forall z R(x,z) \implies z=y)$

1. $\forall x \exists y R(x,y)$ means that the function is not a [[partial function]] i.e. for every $x \in X$ there is a $y \in Y$ that can be brought into relation.\
2.  $(\forall z R(x,z) \implies z=y)$ means that there is a 1 to 1 relationship between the elements of $X$ and $Y$. It is not possible two relate two different objects y and z to the same x
i.e.
is allowed
- R(x,b) -> k
- R(x,n) -> m
is not allowed
- R(x,b) -> k
- R(x,n) -> k

This formula means that no tuples of elements from the source set X should not point to the same element  in the goal set and that all elements of X have a element with which it can be brought into relation.

If one writes:
$R(x)=...$ it means $R(x) = \forall x \exists y R(x,y) \land (\forall z R(x,z) \implies z=y)$

### Example 5:

"$+$ is commutative" $$\phi = \forall x \forall y (x+y=y+x)$$

Learnings $x$ is a three way relation (ternary operation) two inputs x,y point to one output z. One could write this relation also differently

$$\forall x \forall y \forall z \forall z' (+(x,y,z) \land +(x,y,z')) \implies z=z'$$

### Example 6:
"+ admits 0 and inverses"
$$ \phi = \exists x \forall y \exists z (x+y=y \land y+z=x)$$
- $\exists x \forall y x+y=y$ means there are 0 (neutral elements)
- $\exists x \forall y \exists z y+z=x$ means there are inverses 

### Example 7:

'f is continuous'
$$\phi = \forall \epsilon \forall x \exists \delta  \forall y (||x-y|| < \delta \implies ||f(x)-f(y)|| < \epsilon)$$

No free variables!

$$\begin{equation}
  S:
    \begin{cases}
      U^S & = \mathbb{R}\\
      ||...||_2 &\subseteq U^S \times U^S\\
	  +/-  & \subseteq U^S \times U^S \times U^S\\
	  < & \subseteq \subseteq U^S \times U^S \\
	  f & \subseteq  U^S \times U^S
    \end{cases}       
\end{equation}
$$


'f is uniformly continuous'
$$\phi = \forall \epsilon \exists \delta \forall x  \forall y (||x-y|| < \delta \implies ||f(x)-f(y)|| < \epsilon)$$

No free variables

$$\begin{equation}
  S:
    \begin{cases}
      U^S & = \mathbb{R}\\
      ||...||_2 &\subseteq U^S \times U^S\\
	  +/-  & \subseteq U^S \times U^S \times U^S\\
	  < & \subseteq \subseteq U^S \times U^S \\
	  f & \subseteq  U^S \times U^S
    \end{cases}       
\end{equation}
$$

```ad-note 
uniform continuous $\implies$ continuous
Example: \frac{1}{x} is continuous but not uniformly continuous in $\mathbb{R}$
```

Here we got some exercises [[Exercises Verification 7. March class 4]]



