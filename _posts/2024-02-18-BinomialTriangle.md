---
layout: post
title:  "Generating The Binomial Triangle In Haskell"
date:   2024-02-17 10:00:00 +0200
---

This post shows how to "generate" the whole binomial triangle in Haskell using its lazyness and recursion.

The code shown is meant to be run in a jupyter notebook (using [iHaskell](https://github.com/IHaskell/IHaskell) for example). It should also work in GHCI. Of course the code can also be adapted to run in a compiled Haskell file.

The first 6 rows of the binomial triangle look like this:
```
1
1 1s
1 2 1 
1 3 3  1 
1 4 6  4  1
1 5 10 10 5 1
```
For simplicity assume that every row is given as a list containing the numbers of that row (from left to right).
Then the recursive prescription to obtain the row below any given row is the following:
- Let $a$ be the current row with the first element deleted
- Let $b$ be the current row with the last element deleted
- Now construct a new list $c$ by letting its first element be the first element of $a$ added to the first element of $b$ etc. (Here it is understood that $c$ is the empty list if $a$ and $b$ are empty)
- The new row is obtained by appending and prepending a $1$ to $c$

This is simple to implement in Haskell:


```haskell
newRow :: [Int] -> [Int]
newRow oldRow = 1 : zipWith (+) (init oldRow) (tail oldRow) ++ [1]
```

To understand this code:


```haskell
scndRow = [1,2,1]
a =  init scndRow --init returns the list with its last element deleted
print a
b =  tail scndRow -- tail returns the list with its first element deleted
print b
c = zipWith (+) a b -- zipWith (+) takes two lists and adds the elements in the same position of boths list forming a new list
print c
d = 1: c ++ [1] -- 1: prepends a 1 to the list and ++ [1] appends a 1 to the list 
print d
```

    [1,2]

    [2,1]

    [3,3]

    [1,3,3,1]

For example:


```haskell
newRow [1,3,3,1]
```


    [1,4,6,4,1]


Now Haskells lazyness and recursiveness can be used to construct an infinite list containing all rows of the pascal triangle:


```haskell
binomTri = [1] : map newRow binomTri
```

To understand how the above definition works simply (recursively) replace any mention of ```binomTri``` by its definition (this is not Haskell code):
```
binomTri = [1] : map newRow binomTri 
= [1] : map newRow ([1] : map newRow binomTri ) 
= [1] : (newRow [1]) :  map newRow (map newRow ([1] : map newRow binomTri)) 
= [1]: [1,1] : [1,2,1] : ...
```

Now we can obtain a list with the first 7 rows like this:


```haskell
take 7 binomTri
```


    [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1],[1,5,10,10,5,1],[1,6,15,20,15,6,1]]


What follows is some code to "pretty print" the rows of the binomial triangle:


```haskell
padder:: Int -> String
padder n = concat $ replicate n " "
```


```haskell
comp :: String -> String -> String
comp s1 s2 = s2 ++ padder (length s1 - length s2)
```


```haskell
f:: String -> String -> String
f s1 s2 = s1 ++ " " ++ s2
```


```haskell
g = init . foldr f ""
```


```haskell
triPreparer :: [[Int]] -> [[String]]
triPreparer tri = map (zipWith comp (last triString)) triString where triString = map (map show) tri
```


```haskell
binomTriPrinter n = mapM_ (putStrLn . g) (triPreparer tri) where tri = take n binomTri
```

Now the first 20 rows of the binomial triangle can be pretty printed as follows:


```haskell
binomTriPrinter 20
```


    1
    1 1 
    1 2  1  
    1 3  3   1  
    1 4  6   4   1   
    1 5  10  10  5    1    
    1 6  15  20  15   6     1    
    1 7  21  35  35   21    7     1    
    1 8  28  56  70   56    28    8     1    
    1 9  36  84  126  126   84    36    9     1    
    1 10 45  120 210  252   210   120   45    10    1    
    1 11 55  165 330  462   462   330   165   55    11    1    
    1 12 66  220 495  792   924   792   495   220   66    12    1    
    1 13 78  286 715  1287  1716  1716  1287  715   286   78    13    1    
    1 14 91  364 1001 2002  3003  3432  3003  2002  1001  364   91    14    1    
    1 15 105 455 1365 3003  5005  6435  6435  5005  3003  1365  455   105   15    1   
    1 16 120 560 1820 4368  8008  11440 12870 11440 8008  4368  1820  560   120   16   1  
    1 17 136 680 2380 6188  12376 19448 24310 24310 19448 12376 6188  2380  680   136  17  1  
    1 18 153 816 3060 8568  18564 31824 43758 48620 43758 31824 18564 8568  3060  816  153 18  1 
    1 19 171 969 3876 11628 27132 50388 75582 92378 92378 75582 50388 27132 11628 3876 969 171 19 1

