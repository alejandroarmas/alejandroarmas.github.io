+++
title = "Combinations" 
author = "Alejandro Armas"
tags = ["Mathematics"]
date = 2020-05-03
+++


Since the concept of "n choose k" seems to appear a lot in my life I decided I would make a quick post explaining the intuition behind it. Let's start with a simple example. 

Say we had a set of three greek characters representing the names of three friends,  {{< katex " F = \{ \alpha, \beta, \gamma \}" true />}}  and we are interested in knowing how many uniquely paired matches could be played between two competitors of the friends in table tennis. If we began choosing a competitor at random, there would be 3 friends to pick from. The next competitor, there would be only 2 friends to pick from. We can easily see that there are  {{< katex "3 \times 2 = 6" true />}}  ways of choosing competitors  {{< katex "P = \{ (\alpha, \beta) , (\alpha, \gamma), (\beta, \gamma), (\beta, \alpha), (\gamma, \alpha) , (\gamma, \beta) \}" true />}} . The  {{< katex "3 \times 2 " true />}}  can similarly be writted as  {{< katex "\frac{3!}{(3-2)!}. " true />}} As you can see order matters in this pairing and this is called a **Permutation**. We only had  {{< katex "n = 3" true />}}  *friends* to participate in our unique matches of  {{< katex "k = 2" true />}}  *competitors*. In general, we would say the permutations of games denoted by  {{< katex "n" true />}}  *friends* and  {{< katex "k" true />}}  *competitors* is:

 {{< katex >}}  n \times (n - 1) \times \dots \times (n - k - 1) = \frac{n!}{(n - k)!} {{< /katex >}} 

However this does not account for when we have no care for order, because let's face it, if your friend is playing on a specific side, the game should be equal and we won't care the "order" that our equation just accounted for. Consider the possibilities we had from our previous example  {{< katex "P = \{ (\alpha, \beta) , (\alpha, \gamma), (\beta, \gamma), (\beta, \alpha), (\gamma, \alpha) , (\gamma, \beta) \}" true />}} . There seems to be some redundancy and we can remove a few, resulting in  {{< katex "C = \{ (\alpha, \beta) , (\alpha, \gamma), (\beta, \gamma) \}" true />}} . This is called a **combination**. Notice the combination is of size 3 while the permutation is of size 6. You simply divide by  {{< katex "k" true />}}  *competitors* you are considering in this game. Then we can see that a combination is defined by:

 {{< katex >}}  {n \choose k } = \frac{n!}{(n - k)! \cdot k!} {{< /katex >}} 

And there you have it. Permutation deals with ordered arrangements and combinations deals with unordered combinations.
