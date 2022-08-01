# 1 Model Checking problem
input:
- formula $\phi$
- structure $S$ defining a semantic for the tokens of the formular

output:
does the formula hold over $\phi$

[[validity satifiability]] 
input:
- formula $\phi$ $\rightarrow$ checker \rightarrow yes no 
output:
yes/no does $\phi$ hold over all possible S
$\phi$ needs to hold over all S and is more strict than 

[[logical equivalence]]:
input:
formula $\phi_1$
formula $\phi_n$
output:
yes: if $\phi_1$ till $\phi_n$ hold over all S

usefull for:
if $\phi_1$ is very complex and $\phi_2$ is super trivial. If it turns out that they are logically equivalent we can use $\phi_2$ instead of $\phi_1$ and save a lot of calculations.

equivalence reduces to [[validity satifiability]]

```ad-note
$\models$ is equivalent to $\Rightarrow$
and means from that the Righthand side  is the logical consequence of the Lefthand side
```

## 1.1 [[definability between logics]]
input:
- formula $\phi_1$
- Logic $L_1$

Question:
can you rewrite $\phi_1$ valid in $L_1$ to another formula $\phi_2$ in $L_2$ for example because maybe $L_2$ has better algorithmical complexity.

# 2 [[Propositional Logic]]
==vocabulary:==
- $\sum = \{p,q,r\}$ are boolean variables
- $\lor,\land,\neg,\implies,\iff$ are [[boolean connectives]]

==syntax==
grammar: what is a valid formula
examples : $p|q|,|\phi \land \phi|\neg|\phi \implies \phi|$

all formulas can also be represented by a [[syntactic tree]]
example $p \land (\neg q \lor r)$ is

<!-- https://q.uiver.app/?q=WzAsNixbMSwwLCJcXGxhbmQiXSxbMCwxLCJxIl0sWzIsMSwiXFxsb3IiXSxbMSwyLCJcXG5lZyJdLFszLDIsInIiXSxbMSwzLCJxIl0sWzAsMV0sWzAsMl0sWzIsM10sWzIsNF0sWzMsNV1d --> <iframe class="quiver-embed" src="https://q.uiver.app/?q=WzAsNixbMSwwLCJcXGxhbmQiXSxbMCwxLCJxIl0sWzIsMSwiXFxsb3IiXSxbMSwyLCJcXG5lZyJdLFszLDIsInIiXSxbMSwzLCJxIl0sWzAsMV0sWzAsMl0sWzIsM10sWzIsNF0sWzMsNV1d&embed" width="300" height="300" style="border-radius: 8px; border: none;"></iframe>
 
 semantics:
 requires a structure $S: \sum \implies \{true,false\}$
 describes when $\phi$ holds on S (denoted as $S \models \phi$)
 
 examples for the application of $\models$
 $$S \models p \iff S(p)=True$$
 $$ S \models \phi_1 \land \phi_2 \iff S \models \phi_1 \text{ and } S \models \phi_2$$
 $$S \models \phi_1 \lor \phi_2 \iff S \models \phi_1 \text{ or } S \models \phi_2$$
 
# 3 Model Checking
 We write a program that check if the above statements are fulfilled
 
 ```python
def Model-check(phi,S):
	if phi = p:
		return S(p)
	elif phi = phi_1 or phi_2:
		return Model-check(phi_1,S) 
				or Model-check(phi_2,s)
	elif phi = phi_1 and phi_2:
		return Model-check(phi_1,S) 
				and Model-check(phi_2,s)
	elif ...
 
 ```
 
What is the complexity of this algorithm is polynomial:
size of the formula -> number of rows of the [[syntactic tree]] 
times the size of the structure -> polynomial

==Name== EVAL and is p-complete

# 4 [[Satisfiability]]
Short name: ==SAT==
We look for one Structure of $S$ where the 
```python
def Satisfiable(phi):
	let p1,p2,... = all propositional variables in phi
	
	for v1 = true,false do
		for v2 = true,false do
		...
			S=[p1:v1,p2:v2]
			if Model-check(phi,S):
				return true
	return false

```
The complexity is exponential time because you have to try every possible configuration of variables. 

One can guess the inputs $vx$ to make it non-deterministic. Then the complexity is not exponential.

#[[Validity]]
We look if the formula $\phi$ is valid in all Structures $S$
```python
def Valid(phi):
	let p1,p2,... = all propositional variables in phi
	
	for v1 = true,false do
		for v2 = true,false do
		...
			S=[p1:v1,p2:v2]
			if not Model-check(phi,S):
				return false
	return true
```
The complexity is exponential time because you have to try every possible configuration of variables. 

One can guess the inputs $vx$ to make it non deterministic.


# 5 Economy of Syntax
[[Lemma 1]]:
Every formula is equivalent to one without $\iff$ and $\implies$

prove:
$\phi_1 \implies \phi_2$ is equivalent to $(\neg \phi_1) \lor \phi_2$

$\phi_1 \iff \phi_2$ is equivalent to $$(\phi_1 \land \phi_2)\land (\neg\phi_1 \land \neg \phi_2)) $$

[[Lemma 2]]:
Every formula is equivalent to one in [[Negation Normal Form]].
The [[Negation Normal Form]] can be computed efficiently if there is no $\iff$.
$$\neg(\phi_1 \lor \phi_2)$$
 proof: 
 - $\neg(\phi_1 \lor \phi_2)$ becomes $(\neg\phi_1 \land \neg\phi_2)$
 -  $\neg(\phi_1 \land \phi_2)$ becomes $(\neg\phi_1 \lor \neg\phi_2)$

see: [[Morgans Laws]]

[[Lemma 3]]:
Every formula is [[equi-sartisfiable]] to one in [[Conjunctive Normal Form]]. The [[Conjunctive Normal Form]] can be computed efficiently if there is no $\iff$

proof: exercise

[[Corollary 1]]:
CNF-SAT is NP-complete

# 6 [[Tableaux]]
We want to check [[Satisfiability]]
Motto:instead of guessing the structure we guess pieces of the formula that are easy to satisfy.

A [[Tableaux]] is usually a tree.

<!-- https://q.uiver.app/#?q=WzAsNixbMSwwLCJcXHsocCBcXGxvciBcXG5lZyBxKVxcbGFuZFxcbmVnIHBcXH0iXSxbMSwxLCJcXHtwXFxsb3IgXFxuZWcgcSxcXG5lZyBwIFxcfSJdLFswLDIsIlxce3AsXFxuZWcgcFxcfSJdLFsyLDIsIlxce1xcbmVnIHEsXFxuZWcgcFxcfSJdLFsyLDMsIlN1Y2Nlc3MiXSxbMCwzLCJjb250cmFkaWN0aW9uIl0sWzAsMV0sWzEsMl0sWzEsM10sWzMsNF0sWzIsNV1d --> <iframe class="quiver-embed" src="https://q.uiver.app/#?q=WzAsNixbMSwwLCJcXHsocCBcXGxvciBcXG5lZyBxKVxcbGFuZFxcbmVnIHBcXH0iXSxbMSwxLCJcXHtwXFxsb3IgXFxuZWcgcSxcXG5lZyBwIFxcfSJdLFswLDIsIlxce3AsXFxuZWcgcFxcfSJdLFsyLDIsIlxce1xcbmVnIHEsXFxuZWcgcFxcfSJdLFsyLDMsIlN1Y2Nlc3MiXSxbMCwzLCJjb250cmFkaWN0aW9uIl0sWzAsMV0sWzEsMl0sWzEsM10sWzMsNF0sWzIsNV1d&embed" width="280" height="250" style="border-radius: 8px; border: none;"></iframe>

Another example:
<!-- https://q.uiver.app/#?q=WzAsNixbMCwwLCJcXHsgKHAgXFxsb3IgXFxuZWcgcSkgXFxsYW5kIChcXG5lZyBwIFxcbGFuZCBxKSBcXH0iXSxbMCwxLCJcXHtwIFxcbG9yIFxcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDIsIlxce3AsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFsxLDIsIlxce1xcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDMsIlxce3AsXFxuZWcgcCxxIFxcfSJdLFsxLDMsIlxce1xcbmVnIHEsIFxcbmVnIHAscVxcfSJdLFswLDFdLFsxLDJdLFsxLDNdLFsyLDRdLFszLDVdXQ== --> <iframe class="quiver-embed" src="https://q.uiver.app/#?q=WzAsNixbMCwwLCJcXHsgKHAgXFxsb3IgXFxuZWcgcSkgXFxsYW5kIChcXG5lZyBwIFxcbGFuZCBxKSBcXH0iXSxbMCwxLCJcXHtwIFxcbG9yIFxcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDIsIlxce3AsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFsxLDIsIlxce1xcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDMsIlxce3AsXFxuZWcgcCxxIFxcfSJdLFsxLDMsIlxce1xcbmVnIHEsIFxcbmVnIHAscVxcfSJdLFswLDFdLFsxLDJdLFsxLDNdLFsyLDRdLFszLDVdXQ==&embed" width="317" height="280" style="border-radius: 8px; border: none;"></iframe>

Rules:
One can only break up on conjunction or disjunction every level.
The choice changes the tableaux but the result is always the same.
1. $\phi$ needs to be in the [[Negation Normal Form]] -> to keep the $\neg$ next to the variables
2. start with a singleton tree $\{\phi\}$ which in other representation is $\{\alpha_0\}$ with one single leave $F_0$
for each leave that is not _unblocked_:
4. Choose a part of the formula $\alpha_n$ (a sub-formula)
5. expand the tree under $F_n$ by adding
	- if $\alpha_n$ has the form of $\beta \land \beta'$
		- $F_n+1$ = $\{F \text{ ohne } \alpha, \beta,\beta' \}$
	- if  $\alpha_n$ has the form of $\beta \lor \beta'$ add two children
		- $F_{n+1}$ = $\{F \text{ ohne } \alpha, \beta \}$
		- $F_{n+1}$ = $\{F \text{ ohne } \alpha, \beta' \}$
	The formula is not 
	The formula is __invalid__ if one branch contains a contradiction for instance {$p,\neg p$}
	The formula is __valid__ if no branch contains a contradiction
	
	
## 6.1 Example/ Application:
Consider a device whose internal state is encoded by $k$ bits $\underline{p}=p_1,...,p_n$
- initial state is described by a propositional formula $\phi_{init}(\underline{p})$
- target state is described by a propositional formula $\phi_{target}(\underline{p})$
- Transitional formulas are described by a propositional formula $\phi_{step}(\underline{p},\underline{p'})$

Question: can we go from $\phi_{init}(\underline{p})$ to $\phi_{target}(\underline{p})$ by only applying  $\phi_{step}(\underline{p},\underline{p'})$

Maximum length of steps is $2^k$ as there are ony $2^k$ possible variations when having k bits.

The formula describes it:

$$\phi_{reach}(\underline{p_1},....,\underline{p_n})=\phi_{init}(\underline{p_1}) \land \phi_{step} (\underline{p_1},\underline{p_2})\land \text{ ... } \land \phi_{step}(\underline{p_{n-2}},\underline{p_{n-1}}) \land \phi_{target}(\underline{p_n})$$

If this formula is [[validity satifiability|satisfiable]] there is a way from _init_ to _target_


# 7 [[QBF]] Quantified Boolean Formulas
<mark style="background: #014E11F2;">Vocabulary:</mark> 
- Boolean variables $\sum = \{p,q,r...\}$
- Boolean connectives $\land,\lor,\neg,\iff,\implies$
- $\forall,\exists$ Quantifiers

<mark style="background: #014E11F2;">Syntax:</mark> 
$$\phi = p|q|...|\phi \land \phi|\phi \lor \phi|\neg\phi| \phi \iff \phi|\phi \implies \phi|\exists p \phi|\forall p \phi$$

<mark style="background: #014E11F2;">semantics</mark> :
describes when $S \models \phi$ for $S: \sum \implies \{\text{True,False}\}$

| $S \models p$                   | $\iff$ | $S(p)=True$                                                                        |
| ------------------------------- | ------ | ---------------------------------------------------------------------------------- |
| $S \models \phi_1 \land \phi_2$ | $\iff$ | $S \models \phi_1 \text{ or } S \models \phi_2$                                    |
| ...                             |        |                                                                                    |
| $S \models \exists p \phi$      | $\iff$ | $S'\models \phi \text{ for some } S' \in \{S[p:=\text{true}],S[p:=\text{false}]\}$ |
| $S \models \exists p \phi$      | $\iff$ |                     $S'\models \phi \text{ for every } S' \in \{S[p:=\text{true}],S[p:=\text{false}]\}$ |                                                               |


The $\forall$ and $\exists$ means that we fix one of the variables to either true or false and reevaluate it with this fixed value. If $S$ is valid for one of the set values one uses $\exists$ if the structure holds for all one uses $\forall$.

```ad-note 
$\exists p \phi$ is logically equivalente to $\neg \forall p \neg \phi$
```

Example:
$S \overset{?}{\models} \forall p \exists q (p \lor \neg q) \land (\neg p \lor q)$

$S_1=[p:=true] {\models} \forall p \exists q (p \lor \neg q) \land (\neg p \lor q)$ 
two possibilities for S_1 of which one but be satisfied:
$S_1'=[p=true,q=false]$ result with this input is not satisfied
$S_1''=[p=true,q=true]$ result with this input is satisfied => True


$S_2=[p:=false] {\models} \forall p \exists q (p \lor \neg q) \land (\neg p \lor q)$ 
Same here, one of the two options need to be satisfieed 
$S_2'=[p=false,q=false]$ result with this input is satisfied =>true
$S_2''=[p=false,q=true]$ result with this input is not satisfied=>false

That means that means that in case $S''$ there does not exist one $q$ that makes the equation valid that means the whole statement is wrong

```ad-note 
title: Bound and free variables
- a variable p is considered <mark style="background: #014E11F2;">bound</mark> when it appears under a scope of a quantor i.e. $\exists p$ or $\forall p$
- a variable is considered free when it is not in the a scope under quantor. i.e. in all other cases
```
Example:
the first occurence of $p$ is free. The third occurence of p ($\neg p$) is bound to the $\exists p$.
$\phi = p ..... \exists p ....(\neg p)$

==When we write $\phi(p_1,p_2,...,p_n)$== we mean that the free variables of $\phi$ are $p_1,p_2,...,p_n$

==When we write $\phi[p/\alpha]$== we denote a formula where we replace all occurences of $p$ by $\alpha$. Another Notation could be when we first write $\phi(p)$ that to denote that we exchange p by $\alpha$ we write :$\phi[\alpha]$. Take care square brackets!

Example:
$\phi= \neg p \lor \exists p (p \land q)$
When we write $\phi [p/\alpha]$ we only replace the <mark style="background: #014E11F2;">free</mark>  occurences of $p$ 
i.e:
$\phi= \neg \alpha \lor \exists p (p \land q)$

```ad-note
title:[[Lemma 4 (renaming)]]
$\exists p \phi$ is equivalent to $\exists q \phi[p/q]$ if q does not appear ==free== in $\phi$
