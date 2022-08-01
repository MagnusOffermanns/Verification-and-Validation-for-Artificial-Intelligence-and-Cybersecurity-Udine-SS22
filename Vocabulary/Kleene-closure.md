---
aliases: Kleene star 
---

[[Kleene-closure]] of a set $A$ denoted by $A^*$, is defined as:
$$A^*=\bigcup\limits_{u\geq0} A^n= \{\epsilon\}\cup A \cup A \cdot A\cup A\cdot A\cdot A \cup...$$
i.e. all finite words that can be obtained by [[Concatenation]] of $A$ with itself.
In all important cases the result of a [[Kleene-closure]] is a infinite set but consist of finite words.

Example 1:
$A=\{a\}$ 
$A^*=\{\epsilon\} \cup \{a\} \cup \{aa\}...$

Example 2
$A=\{a,b\}$ 
$A^*=\{\epsilon\} \cup \{a\} \cup \{ab\} \cup \{ba\}\cup\{aa\}\cup\{bb\}\cup\{aab\}...$

