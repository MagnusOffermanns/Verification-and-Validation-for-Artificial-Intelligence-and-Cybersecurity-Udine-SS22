---
aliases:
  - Execution Path
---
An [Execution structure](Execution%20structure.md) is a [Directed graph](Directed%20Network.md), whose nodes are all the states that can be reached by executing the actions in the [state-action table](state-action%20table.md) and whose edges represent possible action
executions.

# 1 Total Execution structures

It is not required to be **total**, that is, it may include nodes (states) with no outgoing edges (terminal states).

# 2 Reachability
We say that a state $s'$ is reachable from a state $s$ if there is path from $s$ to $s'$

# 3 [acyclic execution](acyclic%20execution.md)

We say that $K$ is an [[acyclic execution]] structure if all its execution paths are finite.