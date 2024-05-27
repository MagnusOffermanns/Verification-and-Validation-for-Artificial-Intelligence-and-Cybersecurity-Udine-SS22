[[Lemma 3]]:
Every formula is [[equi-sartisfiable]] to one in [[Conjunctive Normal Form]]. The [[Conjunctive Normal Form]] can be computed efficiently if there is no $\iff$

First we convert the formula into [Negation Normal Form](Negation%20Normal%20Form.md). Hereby we have a formula of the form:

$P_1 \land P_2 \dots \land P_n$

Where $P$ is either - 
- a literal (i.e. true or false) or
- a bracket of the following form: $(Q_1 \lor Q_2 \lor \ldots \lor Q_n)$

The formulas $Q$ can again can be literals we have reached the [Conjunctive Normal Form](Conjunctive%20Normal%20Form.md). Otherwise they have the form:
$Q_j = R_1 \land R_2 \land \ldots \land R_m$

Then we use the following formula to resolve the brackets:

$p \lor (q \land r)  \equiv (p \lor q) \land (p \lor r)$


The result are formulas that have the [Conjunctive Normal Form](Conjunctive%20Normal%20Form.md).



