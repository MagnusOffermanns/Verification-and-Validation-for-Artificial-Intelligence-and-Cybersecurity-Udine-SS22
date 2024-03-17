---
aliases:
  - LAR
  - hitting number
---
It is an algorithm to track the states that occur infinitely many times.


We track the occurences of letters, every time we encounter a letter we increase the hitting number. 
1. hitting number $0$
2. hitting number $1$
3. hitting number 2
4. ...

The hitting set contains all letters that we encounter between occurences, ==including the letter itself(as between row 2 and 3, it is only {C})==. Between row 4 and 6 it is for example it is $BD$.

At a certain point the hitting number can not grow beyond a certain value, because there are some states that we just do not encounter anymore.

Then we take the biggest set since the last $n$ steps. The number of last steps is a tuning value.




![](Latest%20Appearance%20Record_image_1.png)