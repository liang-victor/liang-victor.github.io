---
layout: post
title:  "Advent of Code 2022 Day 17 - Pyroclastic Flow"
date:   2023-02-13 12:00:00 -0500
categories: aoc
---

This one involved making tetris, or at least a simplified version of it. Unlike the previous day this one was pretty straightforward to write, not to say I didn't have any problems at all.

In this problem, pieces are falling from the ceiling in a cyclical order, and they're pushed around by jets of hot gas, also in a cyclical order. As pieces come to rest, the next one follows, and it's your task to determine the height of the rock pile after `n` number of rocks have fallen.

```
|······#|  34
|····###|  33
|····###|  32
|··#··##|  31
|··#·###|  30
|###··#·|  29
|··####·|  28
|····##·|  27
|····##·|  26
|····#··|  25
|····#··|  24
|····#·#|  23
|····#·#|  22
|····###|  21
|····#··|  20
|···###·|  19
|····#··|  18
|·####··|  17
|····#··|  16
|····#··|  15
|····#··|  14
|····#··|  13
|··###··|  12
|··###··|  11
|··###··|  10
|··#·#··|  9
|·####··|  8
|··#·#··|  7
|#####··|  6
|··###··|  5
|··###··|  4
|··###··|  3
|····#··|  2
|···###·|  1
|#####··|  0
+=======+
```

Having just learned of bitmasks and bit operations while working on the previous challenge, I decided to implement the internal representation of the chamber and the rocks using them. This choice gave me:
    - an easy way to slide the pieces side to side using the `<<` and `>>` operators
    - a fast way to check for collisions using the `&` operator

Is it the best way? Maybe a more vector based approach would have been more readable and allowed for more operations (i.e. maybe we want to rotate our piece?) but I was glad to be able to practice a new skill. I did see another person's solution using set of complex numbers that was elegantly concise.

What I found tricky was dealing with various off-by-one errors. Is the ground floor at zero or at -1? Does a round start when a piece starts dropping or after it comes to rest? A small error here can make your simulation return the solution from the wrong point in time or measured against the wrong point of reference. As the complexity of the simulation grew I really should have made a few unit tests to keep these issues in check.
