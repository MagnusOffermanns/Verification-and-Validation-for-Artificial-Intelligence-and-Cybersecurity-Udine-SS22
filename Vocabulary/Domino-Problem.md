Also known as tiling problem
<mark style="background: #014E11F2;">input:</mark> 
finite set of 4-sided dominos:
![[Verification 5_image_1.png|300]]
The dominos can either have fields with numbers (dominos with the same number can be connected) or a white field that is used for the border of the rectangle we want to lay.

<mark style="background: #014E11F2;">Goal:</mark> to lay a complete rectangle without holes with the dominos of any size with a __white border__
![[Verification 5_image_2.png|300]]

<mark style="background: #014E11F2;">Special rules:</mark> 
- one does not need to use all the dominos of the set
- One can reuse dominos of the set

This problem is undecidable! No computer can solve it __unless__ we fix the size of the rectangle.

Fun fact: this problem occurs often in literature as one can define a lot of different variants that cover (almost) all complexity classes.

1. NP: One has to tile a square with fixed size n
2. PSPACE: If one has to tile a corridor fixed width n but arbitrary height m
3.Undecidable class:  Arbitrary height and lengthi