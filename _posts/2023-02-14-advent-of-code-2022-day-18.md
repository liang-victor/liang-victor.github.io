---
layout: post
title:  "Advent of Code 2022 Day 17 - Boiling Boulders"
date:   2023-02-14 12:00:00 -0500
categories: aoc
---

In contrast to the previous couple of days this one seemed much simpler! In this problem, we have a list of `(x,y,z)` coordinates representing 1x1x1 cubes. In part 1, I need to determine the surface area of all the cubes, in terms of the number of faces that are exposed. Since some cubes are adjacent to each other, those faces are not exposed.

To solve part 1, I enumerated all the directly adjacent neighbours for each of the given cubes - 6 for each cube. I then iterated through the given cubes and updated my dictionary of neighbours with a count - each representing a two blocks next to each other blocking a face. The two faces blocked from exposure would then be counted once in each neighbour entry. To get the total count of exposed faces, I would then take the maximum possible number of faces exposed (6x the number of cubes) and subtract the number of blocked faces stored in my dictionary.

Part 2 was more interesting. It asks to discount surface area that is internal to the rock. The given example has a simple case - one cube with all faces covered by lava rock cubes. This is fine, but one can quickly think of other examples of internal holes that consist of multiple empty spaces adjacent to each other. It was clear that just looking at the number of faces in contact with lava rock was insufficient.

So instead I thought what if I could name a point clearly on the outside of the rock, then for any empty space next to the rock, if I could navigate my way to that point, then that empty space was also "outside". Then I realized that the external reference point wasn't even that important, I could simply identify clusters of connected empty cubes and reason about which one represented the outside. So my algorithm was as followed:

1. Generate a set of neighbour coordinates out of the input data. Exclude any lava rock cubes.
2. Pop any cube out of the neighbour set.
    a) Use either BFS or DFS to explore all its face adjacent neighbours.
    b) If one of the neighbours is a lava rock, increment my count
    c) Remove neighbours from the neighbour set as I encounter them
3. Once I've found all the connected neighbours of my first chosen cube, pop another cube from the neighbour set and do it again. Repeat until all neighbours have been processed and are grouped by connectivity.

One thing I did have to think about was my definition of neighbour. In my class, I used the term adjacent to describe cubes whose faces were touching my cube, while neighbour was a broader definition allowing for vertex/corner contact. Even so I ran into some issues getting the right answer until I broadened my definition of neighbour to go up to 2 units away in each of x, y and z directions - I guess the input data had some lava rock sections that needed that extra bit of padding to get connected to the main outside set.