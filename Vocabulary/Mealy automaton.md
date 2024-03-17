---
aliases:
  - input-output automaton
---

A [Mealy automaton](Mealy%20automaton.md) $\mathbb{M}$ is:
- a finite state automaton
- with an output function:
	$\tau: S \times \Sigma \to \Gamma$
	- $S$ is the finite set of states
	- $\Sigma$ is a finite input alphabet
	- $\Gamma$ is a finite output alphabet

Given the input sequence:
$$\alpha=\alpha(1),\alpha(2),\dots$$
The output sequence can be denoted as:
$\mathbb{M}=\beta=\beta(1),\beta(2),\dots$

where $\beta(t)$ is calculated by using the output function $\tau$
$$\beta(t)=\tau(\underbrace{\delta^*(s_0,\alpha(0),\dots,\alpha(t-1))}_{\text{defines the current state}},\underbrace{\alpha(t)}_{\text{next transtions}})$$

![](Verification%2043_image_4.png)

- $\delta^*(s_0,\alpha(0),\dots,\alpha(t-1))$
	here is needed to define the current state of the automation. Starting from $s_0$ we input the symbols $\alpha(0)$ till $\alpha(t-1)$ till we are in a certain state for instance $s_x$
- $\alpha(t)$
	Is the symbol ingested last to go from the state reached in $t-1$ i.e. $s_x$ to the next state $s_y$ i.e. the state when we are in state $s_x$ and ingest the symbol $\alpha(t)$
