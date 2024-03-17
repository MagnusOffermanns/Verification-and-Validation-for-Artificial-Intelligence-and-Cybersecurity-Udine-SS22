---
aliases: non-elementary
---

Example:
$$\begin{align}
exp_0(n)&:=n\\
exp_{h+1}(n)&:= 2^{exp_h(n)}\end{align}$$
Whenever one increment by one, we have a exponential gap between the values.

$$\begin{align}
exp_0(n)&:=n\\
exp_{1}(n)&:= 2^{n}\\
exp_{2}(n)&:=2^{2^n}\\
...\\
exp_{h}(n)&:=2^{2^{2^{...^{2^{n}}}}}
\end{align}$$
In the last case we have $h$ occurrences of $2$.

A problem is [[elementary|non-elementary]] when one is not able to find a bound to the tower of exponentials.