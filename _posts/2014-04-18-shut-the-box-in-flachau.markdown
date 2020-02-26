---
layout: post
date: 2014-04-18
title: Shut the box in Flachau
categories: programming
tags: [Java, riddles]
---

Last Christmas I was a few days in the skiing resort
[Flachau](http://www.flachau.at/en/snow-space.html) in Austria to visit a friend. There I
encountered a strange dice game, which I later learned to be “[Shut the
Box](http://en.wikipedia.org/wiki/Shut_the_box)“.

**Problem**: How do you play the game in order to maximize the amount of free coffee you receive?

<!--more-->

{% include image_50.html src='/assets/2014-04-18-shut-the-box/Shut_the_box.jpg'
                         descr='Shut the box situation' %}

The rules of the game are simple. You roll two dice and turn down numbers as long as you
can. The sum of the numbers you turn down must equal the sum of your dice. For example, in
the picture at the right, the only possibility is to turn down the 4. If at the next turn
the player rolls 7, he can turn down either [7], or both [1] and [6]. If you can’t turn
down any more numbers you are bust and your final score is the number shown. If the player
in the picture had rolled 3, he could not go on and would score 14679.  
The player with the lowest score wins.

I played a variant of the game that has no winner, but only a looser --- the player with
the highest score. He then has to pay every other player a coffee at the library we were
playing at. Or something like that, I can’t remember the details...

The whole long night, I was thinking about the proper strategy for this game. Obviously we
are dealing with [partitions of
numbers](http://en.wikipedia.org/wiki/Partition_(number_theory)) here. And what we want to
do, is to minimize the expected value of the final score.  

The probability of some double dice rolls is higher than others (rolling 7 is much more
likely than rolling 2). Also, even the smallest number with five digits is higher than the
highest number with four digits, therefore trying to turn down high numbers is possibly a
bad strategy. We want to turn down *as many numbers* as possible.

The greedy strategy (turning down as many numbers as possible each time) however, is also
obviously a bad one, because the low numbers are more valuable.  
For example, if, on the first turn, we roll 6, turning down [6] is probably a better
strategy than turning down [1],[2], and [3]. If we did the latter, and rolled 2, or 3 any
time after, we’d be bust. Despite thinking about all of this, I could not find a
satisfactory solution.

Therefore, when I returned home late at night from my library tour, I decided to write a
program to find the optimal strategy. The only development environment I had installed on
my laptop was Eclipse for Android. So, unfortunately, Java it was...

For the given problem size (only numbers from 1 to 9), it is easy for a computer to
recursively enumerate the whole decision tree and always pick the move with the lowest
expected score. The optimal decision tree is too big to print here, but you’ll see an
excerpt below (`p_die` is the probability to die after the current state, `EV` is
the expected value for the final score from the current state):

* At the very beginning, your expected score for optimal play is about 14800, and your
  probability to die on the next round is zero (line 1).
* Suppose You roll a 7 at the very beginning. (line 2)
** The optimal strategy here is to just put down the 7.
** The probability to finish on the next dice roll stays zero, i.e., you still
  can cover every possible roll of the dices with the remaining numbers.
** If you keep playing optimally, your expected value now is only 1950.
* The remaining lines show the optimal moves after rolling 7 on the first throw, and the
  state after moving optimally.

Rolls | State                        | p_die | EV
------|------------------------------|-------|----------
  -   | [1, 2, 3, 4, 5, 6, 7, 8, 9 ] | 0.000 | 14765.975
 7    | [1, 2, 3, 4, 5, 6,    8, 9 ] | 0.000 |  1950.347
 7-2  | [1,    3, 4, 5, 6,    8, 9 ] | 0.028 | 40935.389
 7-3  | [1, 2,    4, 5, 6,    8, 9 ] | 0.000 |  2689.550
 7-4  | [1, 2, 3,    5, 6,    8, 9 ] | 0.000 |  1842.870
 7-5  | [1, 2, 3, 4,    6,    8, 9 ] | 0.000 |   580.920
 7-6  | [1, 2, 3, 4, 5,       8, 9 ] | 0.000 |   574.532
 7-7  | [   2, 3, 4, 5,       8, 9 ] | 0.000 |  1383.462
 7-8  | [1, 2, 3, 4, 5, 6,       9 ] | 0.000 |   284.588
 7-9  | [1, 2, 3, 4, 5, 6,    8,   ] | 0.000 |   236.435
 7-10 | [1, 2, 3,    5,       8, 9 ] | 0.000 |   499.984
 7-11 | [1, 2, 3, 4,          8, 9 ] | 0.000 |   354.398
 7-12 | [1, 2, 3, 5, 6,          9 ] | 0.000 |   294.848

The optimal strategy wins 91.5% of the time against three randomly playing opponents. (Of
course the random strategy also wins 75% of the time against three random opponents.) No
one can remember the optimal strategy by heart obviously, because the decision tree is too
large. However, we can try to extract an easy to remember near optimal strategy from the
insights we gained.

The best trade-off strategy I found is quite easy to remember and wins 90.8% of the time
against three random opponents. It is therefore very close to the optimal strategy.

Strategy:

1. Always put down as few numbers as possible.
2. If there are several ways to put down the minimal amount of numbers, use the most
   “central” option.

Rule number two requires a bit of explanation. The most central number is [5], the next
two are [4] and [6], followed by [3] and [7], and so on. It is sufficient to rate
“centrality” separately for each number, starting with the most central one. So if you
rolled 7 and [7] is already gone,  putting down [5] and [2] is better than putting down
[4] and [3], because [5] is more central than [4]. There are only very few cases where it
is not immediately clear which option is more central. As an example here is the order of
moves this strategy proposes if you roll 11, ranked by centrality.

```
[5]-[6]
[4]-[7]
[3]-[8]
[2]-[9]
[2]-[4]-[5]
[1]-[4]-[6]
[2]-[3]-[6]
[1]-[3]-[7]
[1]-[2]-[8]
[1]-[2]-[3]-[5]
```

So if you can, put down [5] and [6]. If this is not possible, try [4] and [7], and so on.
Notice that [1]-[4]-[6] is better than [2]-[3]-[6] in this strategy, because [4] is more
central than [3].

Having found a satisfactory solution, I finally went to sleep at 8 am in the morning.
Unfortunately I never returned to the same library to have some potentially free coffee...
