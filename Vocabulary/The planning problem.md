# Definition

Let $D = (P, S, A, R)$ be a planning domain. A planning problem for $D$ is a triple $(D, I , G )$, where 
- $I \subseteq Q$ is the set of initial states 
- and $G \subseteq S$ is the set of goal states.

Notice that there are two forms of nondeterminism:
-  set of initial states (uncertainty about initial conditions); 
- transition relation (nondeterministic action executions).

The solutions of a planning problem satisfy a reachability requirement: a solution plan is a [state-action table](state-action%20table.md) that, starting at any state in I , allows one to reach a state in $G$.

# 1 [solution](state-action%20table.md)


-  **Weak solutions**:
	SA is a weak solution if, for any state in $I$ , some terminal state of $K$ belonging to $G$ can be reached. This is an *existential condition* only one terminal state needs to be reached.

- **Strong solutions**:
	$SA$ is a strong solution if $K$ is [acyclic](acyclic%20execution.md) and all terminal states of K are in G . We always reach the goal) This is a *universal condition* all terminal states need to be reached.

- **Strong cyclic solutions**:
	$SA$ is a strong cyclic solution to the planning problem if from any state in Q some terminal state of K is reachable and all the terminal states of K are in G (they guarantee the achievement of the goal when the execution is [Fair](Fair.md)”).