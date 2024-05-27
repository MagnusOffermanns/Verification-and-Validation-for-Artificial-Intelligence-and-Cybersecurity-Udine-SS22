Currently at verification 36

# 1 general vocabulary
- [x] [Syntax](Syntax.md)
- [x] [semantics](semantics.md)

- [x] [Tautology](Tautology.md)
- [x] [contradiction](contradiction.md)

- [x] [expressiveness](expressiveness.md)
- [x] [decontain

- [x] [Succinctness](Succinctness.md) vs efficiency

- [x] [Containment problem](Containment%20problem.md)

- [x] [free variables](free%20variables.md)  vs [bound variables](free%20variables.md)

- [x] [Domino-Problem](Domino-Problem.md)

- [x] [Logical reduction](Logical%20reduction.md)

# 2 [Model-checking](Model-checking.md)
- [x] [Validity](Validity.md)
- [x] [Satisfiability](Satisfiability.md)
- [x] [logical equivalence](logical%20equivalence.md)
- [x] [definability between logics](definability%20between%20logics.md)
- [x] [Definability](Definability.md)

# 3 Different logics
## 3.1 [Propositional Logic](Propositional%20Logic.md)
==vocabulary:==
- [x] $\sum = \{p,q,r\}$ are boolean variables
- [x] $\lor,\land,\neg,\implies,\iff$ are [[boolean connectives]]

==syntax==
grammar: what is a valid formula
examples : $p \land q,\phi \land \phi,\neg(\phi \implies \phi)$

## 3.2 [QBF](QBF.md) [Quantified Boolean formulas](QBF.md)

<mark style="background: #014E11F2;">Vocabulary:</mark> 
- [x] Boolean variables $\sum = \{p,q,r...\}$
- [x] Boolean connectives $\land,\lor,\neg,\iff,\implies$
- [x] $\forall,\exists$ Quantifiers

>[!Note] expressiveness
>[QBF](QBF.md) is <mark style="background: #FF5582A6;">not</mark> more [expressive](expressiveness.md) than [Propositional Logic](Propositional%20Logic.md) it only adds [Succinctness](Succinctness.md).

## 3.3 [FO](FO%20-%20First%20order%20logic.md)

<mark style="background: #014E11F2;">Vocabulary:</mark> 
- [x] Boolean connectives $\land,\lor,\neg,\iff,\implies$
- [x] $\forall,\exists$ Quantifiers
- [x] Relationship symbols $\Sigma = {R,S,T}$ (= always in the signature)
- [x] first order variables: $x,y,z$
>[!Note] 
>[Satisfiability](Satisfiability.md) in [FO](FO%20-%20First%20order%20logic.md) is undecidable


## 3.4 Other important definitions
- [x] [elementary equivalence](elementary%20equivalence.md)
	- [x] [Lemma 9](Lemma%209.md)
- [x] [n-equivalent](n-equivalence.md) (in combination with the [Ehrenfeucht-Fraise game](Ehrenfeucht-Fraise%20game.md))
	- [x] [Lemma 10](Lemma%2010.md)
- [x] [Remoteness](Remoteness.md)
- [x] [Hintikka Formula](Hintikka%20Formula.md)


# 4 [Theory](Theory.md)
## 4.1 $FO[\mathbb{N},<]$
## 4.2 $FO[\mathbb{N},+1]$
>[!Note]
> $FO[\mathbb{N},<]$ is more powerful than $FO[\mathbb{N},+1]$ as we can not define a set that only contains $f: n \rightarrow n+1$.
## 4.3 [Presburg arithmetic](Presburg%20arithmetic.md)
$$ FO[\mathbb{N},+]$$
## 4.4 [Peano arithmetic](Peano%20arithmetic.md)
$$FO[\mathbb{N},+,\cdot]$$
## 4.5 [Tarski arithmetic](Tarski%20arithmetic.md)
$$FO[\mathbb{R},+,\cdot]$$
## 4.6 [RadoGraph](RadoGraph.md)

# 5 Normal forms
- [x] [Negation Normal Form](Negation%20Normal%20Form.md)
- [x] [Conjunctive Normal Form](Conjunctive%20Normal%20Form.md)
- [x] [Prenex Normal Form](Prenex%20Normal%20Form.md)

# 6 Games
- [x] [evaluation game](The%20evaluation%20game.md) aka model checking game aka [2-player game](2-player%20game)

- [x] [Ehrenfeucht-Fraise game](Ehrenfeucht-Fraise%20game.md)

## 6.1 Overall game related stuff
- [x] [Strategy](Strategy.md)
- [x] [winning strategy](Strategy.md)
- [x] [Winning region](Strategy.md)
- [x] [positional strategy](Strategy.md)
- [x] [Determined games](Strategy.md)
- [x] [Finite state Strategies](Strategy.md)
- [ ] [Theorem 24](Theorem%2024.md), [Theorem 25](Theorem%2025.md)

# 7 Automata
## 7.1 General vocabulary
- [x] [Kleene-closure](Kleene-closure.md)
	- [x] Difference $A^*$ and $A^+$ [Verification 9](Verification%209.md)
- [x] [Language](Language.md)
## 7.2 [Deterministic Finite State Automata](Deterministic%20Finite%20State%20Automata.md)
- [x]  A [DFA](Deterministic%20Finite%20State%20Automata.md) $\mathcal{A}$ is a tuple $(Q,A,\delta,q_0,F)$ 
- [x] [Acceptance condition](Acceptance%20condition.md) -> end in state $s$ in $F$
- [x] [[Deterministic Finite State Automata#1 Completeness|Completeness]].
- [x] Failure state ([Verification 11](Verification%2011.md)) -> needed to create a complement if [DFA](Deterministic%20Finite%20State%20Automata.md) is incomplete

## 7.3 [Non Deterministic Finite State Atomata](Non%20Deterministic%20Finite%20State%20Atomata.md)
- [x] An [NFA](Non%20Deterministic%20Finite%20State%20Atomata.md) $\mathcal{A}$ is  a tuple ($Q,A,\Delta,q_0,F$) 
	The transition function $\delta$ differes from the [DFA](Deterministic%20Finite%20State%20Automata.md) where:
$$\delta: Q \times A \rightarrow 2^Q$$
- [x] Acceptance condition: There needs to be a chance that the word finishes in a state $s$ of $S$
- [x] [Theorem 2](Theorem%202.md)
- [x] [NFA](Non%20Deterministic%20Finite%20State%20Atomata.md) $\equiv$ [DFA](Deterministic%20Finite%20State%20Automata.md)
## 7.4 [[Non Deterministic Finite State Atomata|NFA]] with $\epsilon$-moves
- [x] Difference to [NFA](Non%20Deterministic%20Finite%20State%20Atomata.md)
	The only difference is $\Delta$
	$\Delta: Q \times (A \cup\{\epsilon\}) \rightarrow 2^Q$
- [x] [epsilon-closure](epsilon-closure.md)
- [x] NFA with epsilon move $\equiv$ [NFA](Non%20Deterministic%20Finite%20State%20Atomata.md) $\equiv$ [DFA](Deterministic%20Finite%20State%20Automata.md)
- [x] The [emptyness problem](emptyness%20problem.md)
- [x] [Universality problem](Universality%20problem.md)
- [x] [Equivalence problem](Equivalence%20problem.md)
- [x] [Containment problem](Containment%20problem.md)
	The equivalence problem can be expressed as two times the containment problem [Verification 12](Verification%2012.md)
- [x] intersection of 1 DFA and 1 NFA -> faster than two DFAs as the complement of NFA can be calculated in Linear time ([Verification 12](Verification%2012.md))
- [x] [Myhill-Nerode Theorem](Theorem%206.md)
- [x] [Equivalence class](Equivalence%20class.md)
- [x] [refine](refine.md)
- [x]  [Myhill-Nerode Theorem](Theorem%206.md) Relativized over a set $T$ ([Verification 13](Verification%2013.md))
- [x] [T-complete](T-complete.md)
- [x] [T-Minimal](T-Minimal.md)

# 8 Finite state automata on infinite words
- [x] [Buechi automata](Buechi%20automata.md)
- [x] [DBA](Buechi%20automata.md) [Deterministic Buechi Automata](Buechi%20automata.md)
- [x] [omega-words](omega-words.md)
- [x] $A^*$
- [x] $A^\omega$
- [x] $A^\infty$
- [x] [w-closure](w-closure.md)
- [x] [Vectorial closure](Vectorial%20closure.md)
- [x] [P-Computation](P-Computation.md)
- [x] [w-regular](w-regular.md)
- [ ] Closure of [Buechi automata](Buechi%20automata.md) i.e. [Theorem 8](Theorem%208.md)
- [x] [w-regular-expression](w-regular.md)
- [x] equivalence of [Buechi automata](Buechi%20automata.md) and [w-regular-expression](w-regular.md)
- [x] [Buechi automata](Buechi%20automata.md) for justice [Verification 20](Verification%2020.md)
- [x] [ultimately periodic w-words](ultimately%20periodic%20w-word.md)
- [x] [emptyness problem](emptyness%20problem.md) for buechi automata [Theorem 10](Theorem%2010.md)
- [x] [Congruence](Congruence.md)
- [x] [Saturation](Saturation.md) and [Theorem 12](Theorem%2012.md)
- [x] The $\approx_{A}$ relation& [Lemma 12](Lemma%2012.md)
- [x] [Theorem 14](Theorem%2014.md) and how we can reduce all of this problems to the [emptyness problem](emptyness%20problem.md)
- [x] [ultimately periodic w-word](ultimately%20periodic%20w-word.md) and how they can be used as a fingerprint of a language, how can they be used to solve the emptyness problem ([Verification 22](Verification%2022.md))
- [x] [decideability](decideability.md) is equivalent to the [emptyness problem](emptyness%20problem.md) and is decidable in [P-Time](P-Time.md)
- [x] Deterministic [Buechi automata](Buechi%20automata.md) are less expressive than non determinstic [Buechi automata](Buechi%20automata.md)
- [ ] [Closure](Closure.md) under union and intersection
- [ ] recognition by a [DBA](Buechi%20automata.md), vectorial closure proposition [Verification 25](Verification%2025.md)
- [ ] [Vectorial closure](Vectorial%20closure.md)
- [ ] [DBA](Buechi%20automata.md)s are not closed under [Complementation](Complementation.md)

# 9 [Muller Automata](Muller%20Automata.md)
- [ ] What is its acceptance condition? And how does it differ from [Buechi automata](Buechi%20automata.md)
- [ ] How to convert a [DBA](Buechi%20automata.md) to a [DMA](Muller%20Automata.md)
- [ ] What is the difference to [Buechi automata](Buechi%20automata.md)? 
	[DMA](Muller%20Automata.md) is closed under boolean operations ([Theorem 18](Theorem%2018.md))
- [ ] [Lemma 14](Lemma%2014.md) -> expression of regular language DMA boolean combination of [Vectorial closure](Vectorial%20closure.md) ([Verification 27](Verification%2027.md))
- [ ] [Mc Naughton Theorem](Theorem%2019.md)
- [ ] [McNaughton and Papert Theorem](Theorem%2021.md)
- [ ] ![](Summary%20for%20learning_image_1.png)

# 10 [Hankel matrices](Hankel%20matrices.md)
[Verification 14](Verification%2014.md)
- [ ] column test word
- [ ] row non relativized [Equivalence class](Equivalence%20class.md)
- [ ] How many rows: States of the minimal automaton

# 11 [Regular Expression](Regular%20Expression.md)s
- [x] [Restricted Regular Expression](Restricted%20Regular%20Expression.md)
- [x] [General Regular Expressions](General%20Regular%20Expressions.md)
- [x] [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md)
- [x] [Restricted Regular Expression](Restricted%20Regular%20Expression.md) $\equiv$ [General Regular Expressions](General%20Regular%20Expressions.md) $\equiv$ Second order logic
- [x] [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md) $\equiv$ [First order logic](FO%20-%20First%20order%20logic.md)
- [x] [Theorem 4](Theorem%204.md)
	[Finite State Automata](Finite%20State%20Automata.md) $\equiv$ [Restricted Regular Expression](Restricted%20Regular%20Expression.md)
- [ ] Closure of [Regular language](Regular%20Languages.md)s
	[Theorem 5](Theorem%205.md)
- [x] [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md) $\equiv$ [Star-free Regular Expressions](Star-free%20Regular%20Expressions.md)
- [x] [n-equivalence](n-equivalence.md)
- [ ] [(n,1)-equivalent](n-equivalence.md)
# 12 [Learning Automata](Learning%20Automata.md)
- [x] [Verification 13](Verification%2013.md)
- [x] [Minimally adequat teacher](Minimally%20adequat%20teacher.md)

# 13 Functions on words
- [ ] What is a function of words
- [ ] [Sequential Transducer](Sequential%20Transducer.md)
- [ ] [monotone functions](monotone%20functions.md)
- [ ] learning algorithm for functions
- [ ] [Myhill-Nerode Theorem](Theorem%206.md) for words [Verification 15](Verification%2015.md)
- [ ] [Hankel matrices](Hankel%20matrices.md) for [monotone word functions](monotone%20functions.md)


# 14 [Fair Transition Systems](Fair%20Transition%20Systems.md)
- [x] [Fair Transition Systems](Fair%20Transition%20Systems.md)
- [x] [Justice](Justice.md) (aka [weak fairness](Justice.md)
- [x] [Compassion](Compassion.md) (aka [strong fairness](Compassion.md)
- [x] [idling transition](idling%20transition.md)
- [x] [diligent transitions](diligent%20transitions.md)
- [x] [P-Computation](P-Computation.md)
	- [x] [Rule of Initiality](Rule%20of%20Initiality.md)
	- [x] [Rule of Consequentiality](Rule%20of%20Consequentiality.md)
	- [x] [Justice](Justice.md)
	- [x] [Compassion](Compassion.md)
- [ ] [P-accessible](P-accessible.md)
- [x] [run](run.md)
# 15 [Simple Programming Language](Simple%20Programming%20Language.md)
- [ ] [Post-location](Post-location.md)
- [ ] [Ancestor relation](Ancestor%20relation.md)
- [ ] [SPL](Simple%20Programming%20Language.md) $\equiv$ [Fair Transition Systems](Fair%20Transition%20Systems.md)
- [ ] control variables [Verification 17](Verification%2017.md)
- [ ] program variables [Verification 17](Verification%2017.md)
- [x] [atomic instruction](atomic.md)
- [x] [Mutual exclusion Problem](Mutual%20exclusion%20Problem.md)
- [x] [Accessibility property](Accessibility%20property.md)
- [x] [Communal Accessibility](Communal%20Accessibility.md)
- [ ] [Safety property](Safety%20property.md)
- [ ] 



# 16 [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)
- [x] [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md)
- [x] [S1S](Monadic%20second%20order%20of%20one%20sucessor.md)
- [x] [WS1S](Monadic%20second%20order%20of%20one%20sucessor.md)
- [x] What is the difference between [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) and [S1SA](Monadic%20second%20order%20of%20one%20sucessor.md)
- [ ] [Open fomulas](Open%20fomulas.md) & [Closed Formulas](Closed%20Formulas.md)
- [ ] `<` and `0` can be defined by the `+1` operator
- [x] what does **monadic**
- [ ] Defining languages in [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) ([Verification 24](Verification%2024.md))
- [ ] [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) closure under projection, [input free automaton](input%20free%20automaton.md)s and the relation to logical sentences [Verification 24](Verification%2024.md)
- [ ] [Buechis-theorem](Theorem%2015.md)
- [ ] [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) is [decidable](decideability.md) ([Corollary 7](Corollary%207.md))
- [ ] conversion of [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) to [Buechi automata](Buechi%20automata.md) and why it is [non-elementary](elementary.md)
- [ ] Special forms of [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) with additonal predicated
	- [ ] is a power of 2 -> decidable
	- [ ] factorical -> decidable
	- [ ] Natural numbers as [degenerate tree](tree.md) ([Verification 25](Verification%2025.md))
	- [ ] Binary tree -> [decideable](decideability.md) ([S2S](The%20monadic%20second%20order%20theory%20of%20two%20successors.md))
	- [ ] $x \cdot 2$ -> covers the entirety of [FO](FO%20-%20First%20order%20logic.md) and [FO](FO%20-%20First%20order%20logic.md) is not decidable
- [ ] [S2S](The%20monadic%20second%20order%20theory%20of%20two%20successors.md) -> can encode also multiple successors 

# 17 [temporal logic](temporal%20logic.md) ([LTL](temporal%20logic.md))
- [ ] $X$
- [ ] $(p)U(q)$
- [ ] $F(p)$ and how it can be defined using only $U$ ([Verification 29](Verification%2029.md))
- [ ] $G(p)$
- [ ] the different kinds of util
- [ ] strong until: $(p)U^{\exists}(q)$
- [ ] non-strict: $(p)U_{\ge}(q)$
- [ ] How does it influence the F,G and U

# 18 Tableux
- [ ] Closure of a formula ([Verification 31](Verification%2031.md))
- [ ] What is an Atom of a formula [Verification 31](Verification%2031.md)
- [ ] [mutually satisfiable](mutually%20satisfiable.md)
- [ ] porposition [mutually satisfiable](mutually%20satisfiable.md), Atoms and Closure and their relation [Verification 31](Verification%2031.md)
- [ ] [Induced Path](Induced%20Path.md)
- [ ] [initial satisfiability](initial%20satisfiability.md)
- [ ] [Promise](Promise.md)
- [ ] [transient node](transient%20node.md) & why a transient subgraph can not be fullfilling
- [ ] [fullfilling Atoms](fullfilling%20path.md) ([Verification 32](Verification%2032.md))
- [ ] [fullfilling path](fullfilling%20path.md)
- [ ] When does a [Tableaux](Tableaux.md) of a formula indicate a model? [Verification 32](Verification%2032.md)?
- [ ] [Tableaux](Tableaux.md) of $\varphi$ and $\neg \varphi$ -> are the same
- [ ] [strongly connected](strongly%20connected.md) subgraph
- [ ] $\varphi$ reachability & [Corollary 8](Corollary%208.md)
- [ ] [Maximal strongly connected subgraph](VV%20Strongly%20connected%20subgraph.md)

# 19 [Model-checking](Model-checking.md) in [LTL](temporal%20logic.md)
- [ ] [local formula](local%20formula.md)s
- [ ] $state(A)$
- [ ] [VV consistent](VV%20consistent.md)
- [ ] [trail](trail.md)
- [ ] [State explosion](State%20explosion.md)
- [ ] [Symbolic model-checking](Symbolic%20model-checking.md)
- [ ] [Ordered Binary Decision Diagramm](Ordered%20Binary%20Decision%20Diagramm.md)
- [ ] [Partial Order reduction](Partial%20Order%20reduction.md)
- [ ] [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) and ordering

# 20 [branching time temporal logic](temporal%20logic.md)
- [ ] Difference [LTL](temporal%20logic.md) and [Branching temporal logic](Branching%20temporal%20logic)
- [ ] $A$ and $E$
- [ ] [CTL*](temporal%20logic.md)
- [ ] The problem with alternating State and path quantifiers, what is the difference with to [CTL*](temporal%20logic.md) ([Verification 35](Verification%2035.md))
- [ ] [path formula](path%20formula.md) and [state formula](state%20formula.md)
- [ ] [LTL](temporal%20logic.md) and [CTL](temporal%20logic.md) are incomparable when looking at expressiveness
- [ ] The set of state formulas is equivalent to the set of [CTL](app://obsidian.md/temporal%20logic.md)/[CTL*](app://obsidian.md/CTL*) formulas. [Verification 35](Verification%2035.md)

# 21 [Model-checking](Model-checking.md) in [CTL](temporal%20logic.md)
- [ ] [fix point](fix%20point.md)
	- [ ] least 
	- [ ] highest fixpoint

# 22 The [Synthesis Problem](Synthesis%20Problem.md)
- [ ] What is the [Synthesis Problem](Synthesis%20Problem.md)?
- [ ] The rules of the synthesis problem: bit-to-bit, finite state solution
- [ ] What are examples of things not possible for the [Synthesis Problem](Synthesis%20Problem.md) [Verification 43](Verification%2043.md)


# 23 [Mealy automaton](Mealy%20automaton.md)
- [ ] [Mealy automaton](Mealy%20automaton.md)
- [ ] [Church's Problem](Church's%20Problem.md)
- [ ] [S1S](Monadic%20second%20order%20of%20one%20sucessor.md) -> [Muller Automata](Muller%20Automata.md) -> [Muller Game](Muller%20Game.md) -> [parity game](parity%20game.md)
- [ ] Whats the difference between [Muller Game](Muller%20Game.md)s, [Weak muller game](Muller%20Game.md)s and [Reachability Games](Muller%20Game.md) ([Verification 43](Verification%2043.md))
- [ ] Solution to [Church's Problem](Church's%20Problem.md) ([Verification 43](Verification%2043.md))
- [ ] [Reachability Games](Muller%20Game.md) & [Theorem 26](Theorem%2026.md)
- [ ] [parity game](parity%20game.md)
	- [ ] Are determined [Theorem 27](Theorem%2027.md)
- [ ] [Game simulation](Game%20simulation.md)s
- [ ] [Latest Appearance Record](Latest%20Appearance%20Record.md)

# 24 Path planning
- [ ] [inertial fluents](fluents.md) and [non-inertial fluents](fluents.md)
- [ ] [Situated plans](Plans.md)
- [ ] [Universal plans](Plans.md)
- [ ] [Conformant Plans](Plans.md)
- [ ] [Deterministic Plan](Plans.md)]
- [ ] The planning domain
- [ ] [state-action table](state-action%20table.md)
- [ ] [Execution structure](Execution%20structure.md)
- [ ] Goal state vs Terminal state


Restricted regular expressions \(\equiv\) General Regular expressions \(\equiv\) Second order logic \(\equiv\) Finite state automata

  

Star free regular expressions \(\equiv\) First order logic