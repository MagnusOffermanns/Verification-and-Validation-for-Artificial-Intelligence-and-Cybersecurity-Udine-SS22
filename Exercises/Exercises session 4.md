Choose appropriate *universes* and *signatures* and define the following properties in FO

## 0.1 There are infinitely many prime numbers
Maybe we can define that every prime number has a prime number that follows?
__Universe:__
$U^S =\mathbb{N}$
__Relations__
$R \subseteq \mathbb{N} = \text{ the prime numbers}$
$< \subseteq \mathbb{N} \times \mathbb{N} (\text{ordering relation})$

Statement -> there are infinitely many prime numbers.
For all numbers of $\mathbb{N}$ there follows a $y$ that is prime
$\phi() = \forall x \exists y (y>x \land R(y))$
Other way but weaker:
for all prime numbers there exists one prime number that follows
$\phi() = \forall x(R(x) \implies \exists y  (y>x) \land R(y))$


## 0.2 This graph is a [[clique]]
nodes and = are the signature

## 0.3 This graph is [[strongly connected]]
This does not work, 
## 0.4 In this tree, z is the least common ancestor of x and y

## 0.5 In this string every a is followed by a b
Universe is a set of numbers denoting the position of the char
Relational symbols are A,B of unary Form
$A = \{2,5,6\} \subseteq U^S$
$B = \{3,9,10\} \subseteq U^S$

## 0.6 Points x,y,z are on the same straight line
Relations we will need:
the + Relation (Addition)
the * Relation (Multiplication) -> the inverse is defined by this as well

$\phi(x_1,x_2,y_1,y_2,z_1,z_2)= \exists w_1,w_2,.... w_1+w_2(x_1-y1)/