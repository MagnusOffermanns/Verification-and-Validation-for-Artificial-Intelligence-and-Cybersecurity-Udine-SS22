# 1 Exercise
Let $A=\{a,b\}$ and let $L=\{ \alpha \in A^\omega: \exists \overset{<\omega}{n} \quad \alpha(n) =a\}$
In words there should be less than infinite positions ($<\omega$) $n$ that have the value $a$. i.e. All words that have a finite number of $a$.

Build a [NBA](Buechi%20automata.md) that recognizes this language:

![](Verification%2027_image_1.png)



# 2 Exercise:
Now we try to build a automaton that accepts the Language that is the complement of the language before.
Let $A=\{a,b\}$ and let $\overline{L}=\{ \alpha \in A^\omega : \exists^{\omega} n \quad \alpha(n)=a\}$ 
i.e. a language that has infinitely many $a$s. Build a [DBA](Buechi%20automata.md) that recognizes $\overline{L}$.

 ![](Verification%2027_image_2.png)

But this is is a [DBA](Buechi%20automata.md) (it has one case for each letter)!

This means that we have a language $L$ that is only acceptable by [NBA](Buechi%20automata.md) but its complement i.e. $\overline{L}$ can be accepted by a less expressive [DBA](Buechi%20automata.md)! From here follows that [DBA](Buechi%20automata.md)s are not closed under [Complementation](Complementation.md).



==Exercise==

It is easy to show that every [DBA](Buechi%20automata.md) is equivalent to a [DMA](Muller%20Automata.md). Whenever there is a [DBA](Buechi%20automata.md) I can build a [DMA](Muller%20Automata.md) that recognizes the same Language.

Let $\mathcal{A}$ be the [DBA](Buechi%20automata.md) $(Q,A,\delta,q_0,F)$. Build an equivalent [DMA](Muller%20Automata.md).

We only need to turn [DBA](Buechi%20automata.md) $F$ into $\mathcal{F}$ of the [DMA](Muller%20Automata.md).

Where $\mathcal{F}=\{P \in 2^Q: P \cap F \neq  \emptyset \}$
($P$ is a subset of $Q$)
We only put in the states that occur infinitely many times. All others do not matter. With [DBA](Buechi%20automata.md) only one of the final states needs to occur infinitely many times. With the [DMA](Muller%20Automata.md) all states in $\mathcal{F}$ need to occur infinitely many times i.e. we put in all states of $F$ that occur infinitely many times and leave the states that do not occur infinitely many times.



Exercise:

lets Express the [DBA](Buechi%20automata.md) from before as a [DMA](Muller%20Automata.md):

![](Verification%2027_image_2.png)

We only need to adapt $F$ to $\mathcal{F}$.
$\mathcal{F}$ must contain all possible subsets of $F$ that contain a final state: 
$$\mathcal{F}=\{\{q_0\},\{q_0,q_1\}\}$$


>[!Proposition] (Exercise)
>[NBA](Buechi%20automata.md) and [NMA](Muller%20Automata.md) have the same expressive power

==Proof==
($\rightarrow$) 
you proceed like in the deterministic case (one needs to define the $\mathcal{F}$)

($\leftarrow$) 
You pass through [S1S](Monadic%20second%20order%20of%20one%20sucessor.md). One takes a [NMA](Muller%20Automata.md) encodes it as [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) function and as we know [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) and [NBA](Buechi%20automata.md) are equivalent, and we know that [NBA](Buechi%20automata.md) and [NMA](Muller%20Automata.md) are equivalent .

$\phi$ of [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) of the form 
$$\exists ... \exists(\phi_1 \land \phi_2 \land \phi_3)$$
Where:
- $\phi_1$ general condition of the initial state (unchanged)
- $\phi_2$ [Rule of Consequentiality](Rule%20of%20Consequentiality.md) (unchanged)
- $\phi_3$ Acceptance condition must be adapted
	How do we encode the acceptance condition in a [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) formula
	We need to constraint the subset of states to occur infinitely many times. And the complement of states to occur a finite many times.
