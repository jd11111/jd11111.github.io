---
layout: post
title:  "Generating All Monotonic Lattice Paths That Do Not Cross The Diagonal In Haskell"
date:   2024-02-24 10:00:00 +0200
---

This post discusses a slightly different problem (for which i do not know a good name) than what it says in the title, 
but part of the solution to that problem will be to do what the title says.  
The problem and how to solve it will be explained in the first section and in the second the solution will be implemented in Haskell.

## Introduction To The Problem

This section of the post introduces the problem that will be solved below in Haskell.

### Weak combinationss

$\def\mod{\operatorname{mod}}$
Let $n \in \mathbb{N}$ be fixed. Consider the set 
$$
S_n:= \bigg \{ (\alpha_1, \dots, \alpha_{n}) \in \mathbb{N}^n : \sum_{i=1}^{n} \alpha_i = n-1 \bigg \}.
$$
The elements of $S_n$ are called weak length $n$ combinations of $n-1$ (in the following i will call them just combinations). 

Any element of $S_n$ can be obtained using the "stars and bars" method:
- there are $2(n-1)$ blank spaces (_)
- choose $n-1$ of them to be stars (in any possible way)
- draw bars on all the other blank spaces
- the bars represent commas of the resulting tuple
- the stars in front/after the bars get summed (with no stars = 0)

Example for $n=4$:

```
_ _ _ _ _ _ -> * * _ _ * _ -> ** ||*| -> (2,0,1,0)
```

Note that there will always be exactly $n-1$ stars and $n-1$ bars.

### Cyclic Group Action

Define the cyclic group of order $n$ by $C_n : = \langle g | g^n = 1 \rangle$.
Then $C_n$ acts on $S_n$ via $g (\alpha_1, \dots, \alpha_n) = (\alpha_n , \alpha_1, \dots, \alpha_{n-1})$.

The goal of this post is to generate an element of each orbit and the number of elements in that orbit using the Haskell programming language.

I will sketch the mathematics that allow to do this.
For the details refer to [this](https://en.wikipedia.org/wiki/Catalan_number).


Consider that any element of $S_n$ can be seen as a length $2n$ list of Bools where a bar
corresponds to False and a star to True (i will refer to such a list as a word).  
We can also view such a list as a lattice path that only moves up (True) and to the right (False).  
Using the [exceedance-decreasing algorithm](https://en.wikipedia.org/wiki/Catalan_number#Third_proof) it can be shown, that the orbit of an element of $S_n$
consists of exactly $n-1$ elements.  
Where it has to be noticed that every step in this algorithm corresponds to acting with $C_n$ elements on the original tuple that defined the path.

For each of these orbits there is a special path, that has exceedence 0 meaning that it does not move above the diagonal.  
Such a path corresponds to $n-1$ pairs of parentheses that are correctly matched where False = opening parenthesis, True = closing parenthesis.  
It follows from there, that such a path corresponds to a full binary tree with $n$ leafs under the isomorphism ```treeToWord``` that is defined in the code below.

## Solving The Problem In Haskell

This section of the post describes how the special members of each orbit of the cyclic group action can be generated in Haskell.
The code is meant to be run in a jupyter notebook using iHaskell.

### Generating All Full Binary Trees With $n$ Leafs

I already described how to generate all full binary trees with $n$ leafs in [this](https://jd11111.github.io/2024/02/18/FullBinTrees.html) blog post.
This is the code to generate them:


```haskell
import Data.Maybe -- will need this later
```


```haskell
data Tree = Leaf | Node Tree Tree deriving Show
```


```haskell
cartProd l1 l2 = [(x,y) | x <- l1, y <- l2] -- cartesian product function, will be used to generate all combinations of left/right subtrees
```


```haskell
treeComb :: ([Tree], [Tree]) -> [Tree]
treeComb (l1, l2) = map (uncurry Node) (cartProd l1 l2) -- given a tuple of list of trees, generate all combinations and create trees by taking the combinations as left/right subtree
```


```haskell
treesWithLeafs :: Int -> [Tree]
treesWithLeafs 1 = [Leaf]
treesWithLeafs n = concatMap treeComb x where x = map (\m -> (treesWithLeafs m, treesWithLeafs (n-m)) ) [0.. n-1]
```


```haskell
treesWithLeafs 3
```


    [Node Leaf (Node Leaf Leaf),Node (Node Leaf Leaf) Leaf]


### Transforming A Tree Into A Word

The following function transforms a tree into the corresponding word:


```haskell
treeToWord :: Tree -> [Bool]
treeToWord Leaf = []
treeToWord (Node t1 t2) = concat [[False],treeToWord t1, [True],treeToWord t2]
```

As an example consider the following:


```haskell
map treeToWord (treesWithLeafs 4)
```


    [[False,True,False,True,False,True],[False,True,False,False,True,True],[False,False,True,True,False,True],[False,False,True,False,True,True],[False,False,False,True,True,True]]


We can see that all of these words correspond to a lattice path that stays below the diagonal (where False =move right and True = move up).

### Turning A Word Into A Combination

The first step to go from a word to a weak combination is to turn the list of bools into a list of lists of bools, where every False is turned into [False]
and all consecutive True values are accumulated into a list.

The following helper function will be needed:


```haskell
accOrSplit :: (a -> a -> Bool) -> a -> [[a]] -> [[a]]
accOrSplit f x l = (x:xs):xss where
  xs:xss = case l of
    (y:_):_ | f x y -> []:l -- if the first element y (which is a list itself) of l is not the empty list and f x y is true, then return []:l which will ultimately lead to the singleton [x] being prepended to l
    _ -> l -- anything else: return l, which will ultimately lead to x being prepended to the first element (list) of l
```

As a simple example consider:


```haskell
print $ accOrSplit (/=) True [[True]] -- /= is the not equal infix operator
print $ accOrSplit (/=) False [[True]]
```


    [[True,True]]



    [[False],[True]]


The following function splits/accumulates a list based on the condition f:


```haskell
splitWhen :: (a -> a -> Bool) -> [a] -> [[a]]
splitWhen f = foldr (accOrSplit f) [[]]
```

We want to accumulate all consecutive trues and split in all other cases:


```haskell
whenChange :: Bool -> Bool -> Bool
whenChange True True = False
whenChange _ _ = True
```


```haskell
splitAtChange ::  [Bool] -> [[Bool]]
splitAtChange = splitWhen whenChange
```

As an example consider:


```haskell
splitAtChange [False,False,True,True,False]
```


    [[False],[False],[True,True],[False]]


Now that all consecutive True values have been accumulated we can transform such a list into the corresponding composition:


```haskell
starsBarsToComp :: [[Bool]] -> [Int]
starsBarsToComp l =  catMaybes [if x== [False] && y == [False] then Just 0 else if x== [False] then Just (length y) else Nothing  |(x,y) <- zippedL] where zippedL = zip l2 (tail l2) where l2 = [False]:l++[[False]]
```


```haskell
starsBarsToComp  (splitAtChange [False,True,False,True])
```


    [0,1,1]


Finally we can define a function that returns a list consisting of one combination of every orbit of the group action:


```haskell
weakComps :: Int -> [[Int]]
weakComps n = map (starsBarsToComp . splitAtChange . treeToWord) (treesWithLeafs n)
```

As an example consider:


```haskell
weakComps 4
```


    [[0,1,1,1],[0,1,0,2],[0,0,2,1],[0,0,1,2],[0,0,0,3]]


We can see, that each of the combinations can not be transformed into another by cyclic shifts.  
Furthermore we can also see that the orbit (under the cyclic group action) of each of the combinations consists of exactly 4 distinct elements as expected.

One way to check for correctness of the code would be to brute force generate all the orbits of the cyclic group action on $S_n$ (for low $n$)
and to compare them (as sets) to the orbits of just the elements that are returned by ```weakComps``` (of course the expectation is equality).
