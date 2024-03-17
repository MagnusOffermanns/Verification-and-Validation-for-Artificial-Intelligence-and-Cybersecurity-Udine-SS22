> [!note]
> $\phi$ has [[Quantifier rank]] n if it has at most n nested quantifiers

The number of Quantifiers is  normally  much smaller than the  [[Quantifier rank]].

The [[Quantifier rank]] is smaller or equal the number of Quantifiers.

Example:
$$\phi = \forall x \forall y(\neg R(x,y) \lor (\exists z R(x,z))\lor(\exists t R(t,y)))$$
$\phi$ has [[Quantifier rank]] 3. 

2 Ranks are because of the two Quantifiers $\forall x$ and $\forall y$ which cover the entire formula.

It is only one Rank for $\exists z$ and $\exists t$ as they are on the same level in the formula when looking at the formula in tree form.

One could resolve the formula to the following making the rank clearer:
$$\phi = (\forall x \forall y \quad \neg R(x,y) \lor (\forall x \forall y\exists z \quad R(x,z))\lor(\forall x \forall y\exists t \quad R(t,y)))$$