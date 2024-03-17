---
aliases:
  - Shannon-Expansions
  - w
---
We use [[Shannon-Expansion]]s
$f(x)=(\neg x \land f|_{x \leftarrow 0}) \lor (x \land f|_{x \leftarrow 1})$

We split $f(x)$ up into two part.
1. Either $x=0$ then we can force $x$ to $0$ i.e. $f|_{x \leftarrow 0}$
2. Or we force $x=1$ then we can force $x$ to $1$ i.e. $f|_{x \leftarrow 1}$

The result are two simpler function that can easier be handled. It looks trivial but is nice for bigger formulas.

Lets say we have a lot o occurences of $x \land y$ and we force $x$ to be 0, we get out two formulas but every occurence of $x \land y$ can be evaluated as $0$ removing complexity.w