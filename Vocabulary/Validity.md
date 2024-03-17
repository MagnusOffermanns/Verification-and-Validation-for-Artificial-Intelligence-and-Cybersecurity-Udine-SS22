<mark style="background: #014E11F2;">Validity:</mark> 	
- formula $\phi$ $\rightarrow$ checker $\rightarrow$ yes no 
output:
yes/no does $\phi$ hold over all possible S
$\phi$ needs to hold over all S and is more strict than the simple model checking problem

a formula is _valid_ if every assignment of values to its variables makes the formula true. For example, $x+3=3+x$ is valid over the integers, but $x+3=y$ is not.

How can we check [Validity](Validity.md)?
We  can reduce it to [Satisfiability](Satisfiability.md).
1. We have a formula $\varphi$ for which we want to check [Validity](Validity.md)
2. We check the [satisfiability](Satisfiability.md) of $\neg \varphi$. 
3. If $\neg \varphi$ is not [satisfiable](Satisfiability.md) it means that $\varphi$ is [Valid](Validity.md)