---
layout: post
title:  "Generating All Full Binary Trees With n Leafs In Haskell"
date:   2024-02-18 10:00:00 +0200
---

This post shows how to generate all full binary trees with a fixed number $n$ of leafs using Haskell.  

The code shown is meant to be run in a jupyter notebook (using [iHaskell](https://github.com/IHaskell/IHaskell) for example). It should also work in GHCI. Of course the code can also be adapted to run in a compiled Haskell file.

The type for a full binary tree can be defined as follows in Haskell:


```haskell
data Tree = Leaf | Node Tree Tree deriving Show
```

So for example the tree (where N stands for node and L for leaf)
~~~
  N  
 / \  
L  N  
  / \  
  L L  
~~~
can be defined as follows:


```haskell
Node Leaf (Node Leaf Leaf)
```

The idea for an algorithm to generate all full binary trees with $n$ leafs (or equivalently $n-1$ nodes) is the following:  

If we are at the root (the first) node, then we must place between $1$ and $(n-1)$ of the leafs on the left subtree.  
If $m$ is the number of leafs placed on the left subtree,
then we must place $n-m$ leafs onto the right subtree.  
This means that we only have to find all trees with $m$ and $n-m$ leafs and then take all possible combinations of $m$ leaf tree on the right and $n-m$ leaf tree on the left.  
This enables the usage of recursion, because $m <n$ and $n-m <n$!

The following two helper functions will enable the recursion:


```haskell
cartProd l1 l2 = [(x,y) | x <- l1, y <- l2] -- cartesian product function, will be used to generate all combinations of left/right subtrees
```


```haskell
treeComb :: ([Tree], [Tree]) -> [Tree]
treeComb (l1, l2) = map (uncurry Node) (cartProd l1 l2) -- given a tuple of list of trees, generate all combinations and create trees by taking the combinations as left/right subtree
```

For example:


```haskell
treeComb ([Node Leaf Leaf, Leaf], [Leaf, Node Leaf (Node Leaf Leaf)])
```


    [Node (Node Leaf Leaf) Leaf,Node (Node Leaf Leaf) (Node Leaf (Node Leaf Leaf)),Node Leaf Leaf,Node Leaf (Node Leaf (Node Leaf Leaf))]


Now here comes the main algorithm, which implements the recursion scheme described above:


```haskell
treesWithLeafs :: Int -> [Tree]
treesWithLeafs 1 = [Leaf]
treesWithLeafs n = concatMap treeComb x where x = map (\m -> (treesWithLeafs m, treesWithLeafs (n-m)) ) [0.. n-1]
```

For example, the 5 trees with 4 leafs are:


```haskell
treesWithLeafs 4
```


    [Node Leaf (Node Leaf (Node Leaf Leaf)),Node Leaf (Node (Node Leaf Leaf) Leaf),Node (Node Leaf Leaf) (Node Leaf Leaf),Node (Node Leaf (Node Leaf Leaf)) Leaf,Node (Node (Node Leaf Leaf) Leaf) Leaf]


As a sanity check we can generate the number of trees with 1,...,12 leafs:


```haskell
x = map (length . treesWithLeafs) [1..12]
```

Which calculates the well known Catalan numbers:


```haskell
x
```


    [1,1,2,5,14,42,132,429,1430,4862,16796,58786]

