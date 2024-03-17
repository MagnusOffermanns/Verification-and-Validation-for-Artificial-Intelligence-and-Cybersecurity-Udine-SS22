$$\{V,\Theta,\mathcal{T}\}$$
- $V=\{u_1,...,u_n\}$ is a set of variables
$V$ is split up into 
	- [[control variables]] -> a variable describing where in the process of the state we are right now
	- [[data variables]] -> data

$\Theta$ is a satisfiable state formula that characterizes the intial state of the system. A state that satisfies $\Theta$ is a initial state.

$\mathcal{T}$ is a finite set of __transitions__
	- each transition $t \in \mathcal{T}$ is a function that maps each state $s$ of $\mathcal{T}$ to a set of states i.e. $t(s)$
	-  $t(s)$ is called a $t-successor$ of s
	- $t$ is enabled in $s$ if $s$ has successor states i.e. $t(s) \neq \emptyset$. In some states $t$ will be enabled in other disabled.

This three components would be a classic [[Transiton System]]

A special case of the [[Transiton System]] is the [[Fair Transition Systems]]. it adds [[Justice]] and [[Compassion]]