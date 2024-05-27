# 1 Expressing strong [Compassion](Compassion.md) in [PLTL](temporal%20logic.md).

p = state is enabled
q = state is taken

$G(F(p)) \land G(F(q))$

- $G(F(p))$: the state is enabled and disabled infinitely many times
- $G(F(q))$: and the state needs to be taken infinitely many times (from time to time)

Solution might also be:

>[!Exercise] Expressing [Compassion](Compassion.md) in [PLTL](temporal%20logic.md).
>$p$: the state is enabled
>$q$: the state is taken
>$G(F(p)) \land F(q)$
>- $G(F(p))$ is only true if $p$ is infinitely many times in the future
>- $F(q)$ is only true if $q$ is true at some point in the future
# 2 Expressing [Justice](Justice.md) in [PLTL](temporal%20logic.md)


p = state is enabled
q = state is taken

$\neg (\neg G(p))U(F(q))$

1. $F(q)$ state will be taken at some point in the future
2. $(\neg G(p))U(F(q))$  We do not want that $G(p)$ stays negative (See the definition of  before ($B$) in the [Verification 30](Verification%2030.md))
3. $\neg (\neg G(p))U(F(q))$ To prevent the step from 2 we negate it

