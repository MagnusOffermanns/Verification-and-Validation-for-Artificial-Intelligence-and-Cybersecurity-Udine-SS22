We are now ready for symbolic model checking.
# 1 Preliminary steps to [Symbolic model-checking](Symbolic%20model-checking.md): [QBF](QBF.md)

[[QBF]] does not increase the [expressiveness](expressiveness) of boolean formulas, but it allows in many cases to write more [Succinct](Succinctness.md) formulas.


What happens if we want to use [Shannon-Expansion](Shannon-Expansion.md) in [QBF](QBF.md)

$\exists x f =f|_{x \leftarrow 0} \lor f|_{x \leftarrow 1}$

$\forall x f =f|_{x \leftarrow 0} \land f|_{x \leftarrow 1}$

We will make use of the following expressions:

$\exists \vec{v}(f(\vec{v},\vec{w}) \land g(\vec{v},\vec{x}))$

This symbolic [Model-checking](Model-checking.md) algorithm called $CHECK$ takes as input a [CTL](temporal%20logic.md) formula and a [Kripke structure](Kripke%20structure.md) structure and returns as output a [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) that represents the set of states where the formula is true.

# 2 CHECK
$CHECK$ is inductively defined on the structure of the formula.

- if $f$ is a [Propositional Letter](Propositional%20Logic) then $CHECK(f)$ returns the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for such a letter.
- if $f$ is $f_1 \land f_2$ or $\neg f_1$, we just apply the algorithm $APPLY$ to the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $f_1$ and  $f_2$
- The only complex case we have to consider  are the ones containing temporal modalities which are
	- $\underbrace{E(X(f_1)),E((f_1)U(f_2))}_{existential}$ and $\underbrace{E(G(f_2)}_{universal}$
- $CHECK(\underbrace{E(X(f_1)}_{CTL formula})$ =$CHECKEX(\underbrace{CHECK(\underbrace{f_1}_{CTL})}_{OBDD})$
	Input($CHECKEX$):  the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) of $f_1$
	output(CHECKEX): the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for $E(X(f_1))$
- $CHECK(E((f_1)U(f_2))$=$CHECKEU(CHECK(f_1),CHECK(f_2))$
- $CHECK(E(G(f_1)))=CHECKEG(CHECK(f_2))$
How does the procedure $CHECKEX$ defined?
	$$CHECKEX(f_1(\vec{v}))=\exists \vec{v}'(\underbrace{R(\vec{v},\vec{v}')}_{OBDD \text{ for } R} \underbrace{\land}_{APPLY} \underbrace{f_1(\vec{v}')}_{OBDD \text{ for } f_1})$$
	Then we need to write the $\exists$ using the algorithm $RESTRICT$
- CHECK $EU$:
	It is based on the algorithm for the least fix point computation for modality $EU$ ([Verification 37](Verification%2037.md)). What does this mean:
	$E(f_1 \lor f_2)=$
	$\mu z.f_2 \lor (f_2 \land E(X(z)))$
	Here the $f_2$ are [OBDD](Ordered%20Binary%20Decision%20Diagramm.md)s we already have.
	We can can calculate $E(X(z))$ for the current state of $z$.
	The algorithm returns in each step of the procedure [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) for the current set of states.
- $E(G(f_1))$:
	The function is defined as the greatest fixpoint of the following function. 
	$vz.f_1 \land E(X(Z))$