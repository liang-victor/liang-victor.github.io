---
layout: post
title:  "Advent of Code 2023 Day 1 - Using Kotlin This Year"
date:   2023-12-03 19:00:00 -0500
categories: aoc
---

I'm back!

As December has arrived it's time to try to Advent of Code problems once again. This time I'm going to use it to try to learn a new language. My language of choice is Kotlin, because maybe it would be nice to make some kind of android app for fun once I know the basics.

The Kotlin team was nice enough to create a github template providing some basic scaffolding for loading the input files and calling functions to run each day's code. Jumping into the first day, I found myself wrestling with the different syntax and style, but I suppose that happens with every new language. 

For part 1, I used map and filter methods for working with enumerables. I found the syntax for those techniques were a bit different from what I'm used to:

```kotlin
input.map { first_and_last_digit(it) }
```

compared to something like this in elixir, it uses the special curly braces to define your mapping function and automatically uses the `it` variable for each item in the enumerable.

```elixir
input | Enum.map(&first_and_last_digit/1)
```

Part 2 was when I started running into some new challenges. As a language, Kotlin cares quite a bit about null safety. For instance, in this part I needed to look for certain substrings in the input. As I was writing this code, the IDE was giving me warnings that certain values could be null - and I needed to deal with it in order to run the code.

A couple of options I learned:
    - I can use a `?` to type results as nullable or conditionally allow certain operations to occur if acting on a non-null value
    - I can use `!!` to throw an exception on a null value

From a beginner's perspective there was a bit more to learn about the type system just to be able to get my code to run. That was a bit frustrating. However, it did help me catch some issues, such as how I was supposed to handle not finding any of the particular substrings in the input I was looking for, so for that it was helpful.