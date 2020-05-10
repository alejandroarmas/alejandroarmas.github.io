---
layout: article
title: Combinations
tags: Mathematics
aside:
    toc: true
  
---

Since the concept of "n choose k" seems to appear a lot in my life I decided I would make a quick post explaining the intuition behind it. Let's start with a simple example. 

Say we had a set of three greek characters representing the names of three friends, $ F = \{ \alpha, \beta, \gamma \}$ and we are interested in knowing how many uniquely paired matches could be played between two competitors of the friends in table tennis. If we began choosing a competitor at random, there would be 3 friends to pick from. The next competitor, there would be only 2 friends to pick from. We can easily see that there are $3 \times 2 = 6$ ways of choosing competitors $P = \{ (\alpha, \beta) , (\alpha, \gamma), (\beta, \gamma), (\beta, \alpha), (\gamma, \alpha) , (\gamma, \beta) \}$. The $3 \times 2 $ can similarly be writted as $\frac{3!}{(3-2)!}. $As you can see order matters in this pairing and this is called a **Permutation**. We only had $n = 3$ *friends* to participate in our unique matches of $k = 2$ *competitors*. In general, we would say the permutations of games denoted by $n$ *friends* and $k$ *competitors* is:

$$ n \times (n - 1) \times \dots \times (n - k - 1) = \frac{n!}{(n - k)!}$$

However this does not account for when we have no care for order, because let's face it, if your friend is playing on a specific side, the game should be equal and we won't care the "order" that our equation just accounted for. Consider the possibilities we had from our previous example $P = \{ (\alpha, \beta) , (\alpha, \gamma), (\beta, \gamma), (\beta, \alpha), (\gamma, \alpha) , (\gamma, \beta) \}$. There seems to be some redundancy and we can remove a few, resulting in $C = \{ (\alpha, \beta) , (\alpha, \gamma), (\beta, \gamma) \}$. This is called a **combination**. Notice the combination is of size 3 while the permutation is of size 6. You simply divide by $k$ *competitors* you are considering in this game. Then we can see that a combination is defined by:

$$ {n \choose k } = \frac{n!}{(n - k)! \cdot k!}$$

And there you have it. Permutation deals with ordered arrangements and combinations deals with unordered combinations.