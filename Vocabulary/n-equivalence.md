---
aliases:
  - n-equivalent
  - (n,1)-equivalent
  - (n,1)-equivalence
---
# 1 n-equivalence
$S,S'$ are n-equivalent if for every $\phi$ with [[Quantifier rank]] n the following holds true: $S \models \phi \iff S' \models \phi$

# 2 (n,1)-equivalence

- $\equiv_{(n,1)}$ (n,1)-equivalence
	The equivalence relation $\equiv_{(n,1)}$ over $A^* \times \mathbb{N}$ is defined as follows: for all $u,v \in A^*$ and $r,s \in \mathbb{N}$:
	$(u,r)\equiv_{(n,1)}(v,s)$ if and only if $(u,r)$ and $(v,s)$ satisfy the same formulas $\phi(x)$ of quantifier depth $n$

To deal with formulas with free variables (one in our case) we consider words with one distinguished position, that is, pairs $(u,r)$ with $u \in A^*$ and $1 \le r \le |u|$

