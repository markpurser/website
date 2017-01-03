---
layout: post
title: "Haskell Christmas Everybody"
author: Mark Purser
date: 2017-01-03 12:05:35 +0000
comments: true
categories: [Functional Programming, Haskell]
published: true
---

Here is my solution to one of the exercises set by our Haskell reading group: Draw a Christmas tree to the console, given the height of the tree as input. It demonstrates some of the Input and Output of Chapter 9 of [Learn You A Haskell For Great Good](http://learnyouahaskell.com). Thanks to [Functional Brighton](https://www.meetup.com/Functional-Brighton) for all the great meet-ups this year

<!-- more -->

In terms of tree decoration we are going for a minimalist approach:

```
runhaskell xmas 4

    *
   ***
  *****
 *******
    |
```

To model the tree, we draw from two sets of integers of equal length. The first being the number of spaces preceding each row - simply starting at height-1 and decrementing to 0 (the last row of the tree, discounting the trunk)

``` haskell
nspaces :: Int -> [Int]
nspaces a = reverse $ take a [0..]
```

The second set of integers represent the stars that make up the actual tree. The set consists of the odd numbers starting from 1. These are generated using a list comprehension:

``` haskell
nstars :: Int -> [Int]
nstars a = take a [x | x <- [1..], odd x]
```

Now we simply zip these two sets together into a list of tuples:

``` haskell
let treemodel = zip (nspaces height) (nstars height)
```

And run them through a stringifyer, converting each tuple to a number of space characters followed by a number of stars characters:

``` haskell
stringifytreerow :: (Int, Int) -> [Char]
stringifytreerow (nspaces, nstars) = (take nspaces $ repeat ' ') ++ (take nstars $ repeat '*')
```

And now to the whole point of the IO chapter! To display something... it's simple using mapM_ which maps putStrLn over all tree strings, and sequences the resulting IO actions. We also display the tree trunk at the same time:

``` haskell
mapM_ putStrLn $ treestrings
putStrLn trunkstring
```

## Limitations

The program does not check for invalid input, such as height 0

## Full listing

{% gist 18ef346fcbd509e4b3ed4342048a9bb6 xmas.hs %}
