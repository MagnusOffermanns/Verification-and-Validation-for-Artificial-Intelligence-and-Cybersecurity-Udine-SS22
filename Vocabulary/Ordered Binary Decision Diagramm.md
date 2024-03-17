---
aliases:
  - OBDD
---
They are a reduced version of [Decision Tree](Decision%20Tree.md)s for boolean function

![](Verification%2037_image_2.png)

Starting from a normall [Binary Decision Diagram](Binary%20Decision%20Diagram.md)

- Merge any [isomorphic](https://en.wikipedia.org/wiki/Graph_isomorphism "Graph isomorphism") subgraphs.
- Eliminate any node whose two children are isomorphic.

# 1 Canonical form
Is the [OBDD](Ordered%20Binary%20Decision%20Diagramm.md) most simplified i.e. with the least nodes and edges.