We want to check [[Satisfiability]]
Motto:instead of guessing the structure we guess pieces of the formula that are easy to satisfy.

A [[Tableaux]] is usually a tree.

Example:
<!-- https://q.uiver.app/#?q=WzAsNixbMCwwLCJcXHsgKHAgXFxsb3IgXFxuZWcgcSkgXFxsYW5kIChcXG5lZyBwIFxcbGFuZCBxKSBcXH0iXSxbMCwxLCJcXHtwIFxcbG9yIFxcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDIsIlxce3AsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFsxLDIsIlxce1xcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDMsIlxce3AsXFxuZWcgcCxxIFxcfSJdLFsxLDMsIlxce1xcbmVnIHEsIFxcbmVnIHAscVxcfSJdLFswLDFdLFsxLDJdLFsxLDNdLFsyLDRdLFszLDVdXQ== --> <iframe class="quiver-embed" src="https://q.uiver.app/#?q=WzAsNixbMCwwLCJcXHsgKHAgXFxsb3IgXFxuZWcgcSkgXFxsYW5kIChcXG5lZyBwIFxcbGFuZCBxKSBcXH0iXSxbMCwxLCJcXHtwIFxcbG9yIFxcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDIsIlxce3AsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFsxLDIsIlxce1xcbmVnIHEsXFxuZWcgcCBcXGxhbmQgcVxcfSJdLFswLDMsIlxce3AsXFxuZWcgcCxxIFxcfSJdLFsxLDMsIlxce1xcbmVnIHEsIFxcbmVnIHAscVxcfSJdLFswLDFdLFsxLDJdLFsxLDNdLFsyLDRdLFszLDVdXQ==&embed" width="634" height="560" style="border-radius: 8px; border: none;"></iframe>


Rules:
One can only break up on conjunction or disjunction every level.
The choice changes the tableaux but the result is always the same.
1. $\phi$ needs to be in the [[Negation Normal Form]] -> to keep the $\neg$ next to the variables
2. start with a singleton tree $\{\phi\}$ which in other representation is $\{\alpha_0\}$ with one single leave $F_0$
for each leave that is not _unblocked_:
4. Choose a part of the formula $\alpha_n$ (a sub-formula)
5. expand the tree under $F_n$ by adding
	- if $\alpha_n$ has the form of $\beta \land \beta'$
		- $F_n+1$ = $\{F \text{ ohne } \alpha, \beta,\beta' \}$
	- if  $\alpha_n$ has the form of $\beta \lor \beta'$ add two children
		- $F_{n+1}$ = $\{F \text{ ohne } \alpha, \beta \}$
		- $F_{n+1}$ = $\{F \text{ ohne } \alpha, \beta' \}$
	The formula is not 
	The formula is __invalid__ if one branch contains a contradiction for instance {$p,\neg p$}
	The formula is __valid__ if no branch contains a contradiction
	
	