---
aliases:
  - Situated plans
  - Universal plans
  - Conformant Plans
  - Deterministic Plan
---
[Situated plans](Plans.md)
	The evolution of the plan may be influenced by the environment. Environmental parameters are repeatedly measured, and the selection of the action to execute takes into account such measurements (**trial and error strategies**). One can get stuck in a state and might need to backtrack

- [Universal plans](Plans.md) (A special case of Situated plans)
	Universal plans associate at least one action with any possible state of the domain. In any system configuration, it is thus possible to find a planned action to execute, we never get stuck. We can always act, no **Backtracking**.

- [Conformant Plans](Plans.md)
	In conformant plans, there is no need to collect any piece of information during the execution of the plan in order to achieve the goal. They are useful when observations of the environment are not possible (**null observability**).
- Deterministic plan
	**Deterministic plans**: for each $s \in S$, there is at most one pair $(s, a) \in SA$. 