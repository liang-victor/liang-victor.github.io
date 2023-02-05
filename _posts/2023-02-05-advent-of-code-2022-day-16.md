---
layout: post
title:  "Advent of Code 2022 Day 16 - Proboscidea Volcanium"
date:   2023-02-05 12:00:00 -0500
categories: aoc
---

I had started working on some of the problems in [Advent of Code 2022](https://adventofcode.com/2022) over the holidays and into early January. The challenges are quite fun and educational, but eventually I found myself stuck at day 16.

It's a graph problem where each node is a valve that can release some amount of pressure per minute once open (all valves are initially closed). The objective is to determine the maximum pressure I can release within 30 minutes given that it takes 1 minute to traverse to an adjacent valve and 1 minute to open a valve.

<img src="/docs/assets/aoc2022-16/problem.gif" height=400>

Some of the challenges here include:
    - your path sometimes has to backtrack over previously visited valves e.g. there are valves at the end of dead ends 
    - there can be value in going by low pressure valves without opening them if it means opening a high pressure valve sooner (maybe you can open them while backtracking?)
 
I had a hard time figuring out how to do this one on my own, and I ended up pausing progress on the challenge for a few weeks. Eventually I decided to [look up a solution by hyper-neutrino](https://www.youtube.com/watch?v=bLMj50cpOug&ab_channel=hyper-neutrino) because I might as well learn something. Here's what I learned:

### Breaking the problem up
While the given graph is unweighted, quite a number of the nodes provide zero pressure. We can traverse this graph and generate a weighted graph comprised of the key nodes that have a pressure value above zero. This can then be the basis for picking the best sequence of key node visits to maximize pressure release.

My mistake initially was trying to do both of these things at the same time - traverse the graph and optimize the path. This was too complicated compared to having two more focused problems to solve.

### DFS works well with memoization
The final solution uses a depth-first search and recursion. The nice thing about this is that you can save some time here by saving results to a cache. In python, this can be as easy as using the `@cache` decorator from the standard library `functools` above your recursive function definition.

### Magic with bitmasks
We need to keep track of the state of the open/closed valves. Initially I had created a class for managing this state, but I ended up learning a more streamlined representation using bit masks (I had never properly learned bit operators before!)

Each valve can be represented by a bit, 1 for open, 0 for closed

```code
Get a value via &
    1010001   valve state
   &0010000   bit mask
=   0010000   result is true!
```

```code
Set a value via |
    1010001   valve state
   |0100000   bit mask
=   1110001
```
I can get the bit mask by left shifting (`<<`) 1 by an appropriate number of index positions. The bit operator approach was also very handy in part 2 because I could use an exclusive-or (`^`) to invert the state of the valves. Bit operations always looked intimidating because of unfamiliarity, but it turns out it's not that bad once you learn the basics of it.