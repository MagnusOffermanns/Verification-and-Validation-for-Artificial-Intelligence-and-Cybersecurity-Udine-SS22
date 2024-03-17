# Closure of sets
For instance:
[[Regular Languages]] are closed under [[Boolean Operations]] ($\cup,\cap,\neg$), [[Concatenation]] and the [[Kleene-closure|Kleene star]].

What does it mean: If you have two regular language and you apply one of the operators the result is still a regular language.


# 1 Closure of formulas
We look for the smallest set of formulas that fullfill the following requirements:
1. $\varphi \in \phi_\varphi$
	My formula is part of the closure
2. for every $p \in \phi_\varphi$ and subformula $q$ of $p$ it holds that $q \in \phi_\varphi$
	Every subformula of our formula is part of the closure
3. for every $p$ \in $\phi_\varphi$ it holds that $\neg p \in \phi_\varphi$ and that $\neg\neg p \equiv p$
	Not only our formula but also its negation is in the closure
4. for every $\psi \in \{G(p),F(p),(p)U(q)\}$ if $\psi \in \phi_\varphi$ then $X(\psi) \in \phi_\varphi$
	==Attention specific for [temporal logic](temporal%20logic.md)== 
	For every formula of the form $\{G(p),F(p),(p)U(q)\}$ part of our set $\phi_\varphi$, we need to add the respective next operator. That means: for $G(P)$ we need to add $X(G(p)$, for $F(P)$ we need to add $X(F(P))$ and so on.