---
layout: post
title:  "Introduction To The Abstract Index Notation And The Sympy Tensor Module"
date:   2023-06-23 11:14:45 +0200
categories:
---
In this post i will explain the abstract index notation for tensors and show how to use the basic features of the Sympy Tensor module, which is  based on using the abstract index notation.

The following topics are covered:

- [The Abstract Index Notation](#the-abstract-index-notation)
- [Tensors in Sympy](#tensors-in-sympy)
    - [Basic Tensor Operations](#basic-tensor-operations)
    - [Coefficient Matrices Of Tensor Expressions](#coefficient-matrices-of-tensor-expressions)
    - [Symmetries Of Tensors And Canonicalization](#symmetries-of-tensors-and-canonicalization)
    - [Symmetrization Of Tensors In Sympy](#symmetrization-of-tensors-in-sympy)


# The Abstract Index Notation

In this section i will briefly explain the abstract index notation for tensors with examples, these examples generalize in obvious ways. The reader is assumed to have some knowledge on the tensor product of vector spaces.

Let $V$ be a finite dimensional vector space and $V^*$ be its dual space. 

The notation $V_{a\ \ \ d}^{\ bc}$ is used for the tensor product $V^*  \otimes V\otimes V \otimes V^*$.
A tensor in $V_{a\ \ \ d}^{\ bc}$ is for example denoted as $T\mathstrut_{a}\mathstrut^{bc}\mathstrut_d$.

### Contractions

The contraction of the first and second factor applied to $T\mathstrut_{a}\mathstrut^{bc}\mathstrut_d$ is denoted by $T_{a\ \ \ d}^{\ ac} \in V^c_{\ \ d}$.

### Product Of Tensors

We have a natural identification $V_{a\ \ \ d}^{\ bc} \otimes V_{ef}^{\; \; g} =V\mathstrut_a\mathstrut^{bc}\mathstrut_{def}\mathstrut^g$.
If $S\mathstrut_{ef}\mathstrut^g \in  V_{ef}^{\; \; g} $ then the notation $T\mathstrut_a\mathstrut^{bc}\mathstrut_{d} S\mathstrut_{ef}\mathstrut^g$ is used for the tensor that is associated to $T\mathstrut_a\mathstrut^{bc}\mathstrut_{d}  \otimes S\mathstrut_{ef}\mathstrut^g$ under this identification.

It is important that the letters in the indices of the two factors are different, because else a contraction would be implied.

### Type Changing

 If $V$ is naturally isomorphic to its dual space  (for example if $V$ is a Hilbert space), then we can identify $V$ and $ V^* $ and therefore change the type of the factors of $V$ and $V^* $  in a tensor product at will. We indicate this by changing the latin index from upper to lower or vice versa.
 
 So for example $T\mathstrut_{ab}\mathstrut^{c}\mathstrut_d \in V\mathstrut_{ab}\mathstrut^{c}\mathstrut_d $ is the tensor corresponding to $T_{a\ \ \ d}^{\ bc}$ after the second factor in the tensor product has been changed from $V$ to $V^*$.

### Rearranging Factors

We can also rearrange the factors of the original tensor product in any order and the resulting tensor product can be indentified with the original. 
 
 For example if we switch the first and the last factor in $V_{a\ \ \ d}^{\ bc}$ we denote the result by $V_{d \ \ \ a}^{\ bc}$ and the tensor in $V_{d \ \ \ a}^{\ bc}$ that corresponds to $T\mathstrut_{ab}\mathstrut^{c}\mathstrut_d $ is denoted by $T\mathstrut_{db}\mathstrut^{c}\mathstrut_a $.

 ### Symmetrizing Of Tensors

Lastly we can (anti) symmetrize a tensor.
For example we denote the symmetrization of the second and third factor of $T\mathstrut_{a}\mathstrut^{bc}\mathstrut_d$ by $T\mathstrut_{a}\mathstrut^{(bc)}\mathstrut_d$. The anti-symmetrization of the same factors is denotes as $T\mathstrut_{a}\mathstrut^{[bc]}\mathstrut_d$.
If we want to exclude some factors between indices we use two vertical bars surrounding the excluded factors. So for example $T\mathstrut^{[a|b|c]}\mathstrut_d$ is the anti-symmetrization of the first and third factor (excluding the second) of $T\mathstrut^{abc}\mathstrut_d$.

# Tensors in Sympy

In this section i will explain to you how to create tensors in sympy (using the abstract index notation) and how to perform the tensor operations described in the preceding section.

After that i will show how to obtain coefficient matrices of the results of such symbolic computations.


```python
from sympy.tensor.tensor import TensorIndexType, TensorHead, tensor_indices #import needed stuff
from sympy.combinatorics import Permutation
```

We can create a sort of "base space" $V$ using the following:


```python
V= TensorIndexType('V', dummy_name='V')
```

Let's create some Latin indices that will function in the same way as explained in the first section:


```python
a, b,c,d,e,f,g  = tensor_indices('a, b,c,d,e,f,g', V) #create two indices associated to V (the same as the abcde etc above)
```

Now to define an actual tensor on $V$ there is another step:


```python
T = TensorHead("T", [V,V]) #define a tensor "base" that is like the T of T^{ab}, note that this is not a tensor but it specifies how many indices there are (2 here, but they could be up or down)
S = TensorHead("S", [V,V]) 
```

The type (upper/lower indices) is indicated by inserting a minus for a lower index as follows:


```python
T(a,-b) #this is a tensor with one upper and one lower index
```




$\displaystyle T{}^{a}{}_{b}$




```python
T(a,b) #two upper indices
```




$\displaystyle T{}^{ab}$




```python
5*T(a,b) #scalar multiply the tensor
```




$\displaystyle 5T{}^{ab}$

## Basic Tensor Operations

The four basic operations product, sum, contraction and rearrangement are implemented as follows:


```python
T(a,b)*S(c,-d) #the product of the two tensors
```




$$\displaystyle T{}^{ab}S{}^{c}{}_{d}$$




```python
T(a,b)+S(a,b) #the sum of two tensors
```




$$\displaystyle S{}^{ab} + T{}^{ab}$$




```python
T(a,b)*S(-b,c) # the contraction of the two tensors (dummy index used for the contracted slots, since the output only has 2 slots (a,c))
```




$$\displaystyle T{}^{aV_{0}}S{}_{V_{0}}{}^{c}$$




```python
T(b,a) #rearrange T^{ab} to T^{ba}
```




$$\displaystyle T{}^{ba}$$



When we want to rearrange a tensor expression we can do it as illustrated by the following example (the same works for arbitrary tensor expressions):


```python
expr = T(a,b)+ S(a,b)
expr
```




$$\displaystyle S{}^{ab} + T{}^{ab}$$




```python
expr._replace_indices({a:b, b:a}) #supply a dictionary of replacements (these can be arbitrary not just interchange)
```




$$\displaystyle S{}^{ba} + T{}^{ba}$$



We can also change the type of a tensor expression in the same way


```python
expr._replace_indices({a:-a, b:b}) #lower the first index
```




$$\displaystyle S{}_{a}{}^{b} + T{}_{a}{}^{b}$$



## Coefficient Matrices Of Tensor Expressions

Often we not only want to manipulate symbolic tensor expressions, but we also want the coefficient matrix of the resulting tensors. We can set coefficient matrices and insert them into an expression. Note that the syntax is allways the same for any tensor expression.


```python
repl = {T(a,b) : [[1,2],[5,6]], S(c,d) : [[8,1],[2,9]]} #assign a coefficient matrix to the tensors T(a,b) and S(c,d) representing them in some (common) basis
```


```python
T(a,b).replace_with_arrays(repl) #the coefficient matrix of T^{ab}
```




$$\displaystyle \left[\begin{matrix}1 & 2 \\ 5 & 6\end{matrix}\right]$$



The coefficient matrix of the sum is obtained like this:


```python
sum = T(a,b)+S(a,b)
sum
```




$$\displaystyle S{}^{ab} + T{}^{ab}$$




```python
sum.replace_with_arrays(repl) #the coffiecient matrix of the sum 
```




$$\displaystyle \left[\begin{matrix}9 & 3\\7 & 15\end{matrix}\right]$$



To lower and increase indices the coefficient matrix of the metric must first be given:


```python
repl.update({V: [[-1,0],[0,1]]}) #this specifies the coefficient matrix of the metric to the same common basis
```


```python
T(a,-b).replace_with_arrays(repl) #here the metric is used to lower the index b
```




$$\displaystyle \left[\begin{matrix}-1 & 2 \\-5 & 6\end{matrix}\right]$$



The coefficient matrix of the tensor product of two tensors in the abstract index notation can be obtained as well:


```python
E = TensorHead("E", [V]) #define a base with one index
F = TensorHead("F", [V]) 
```


```python
repl.update({E(c):[1,2], F(d):[5,6]}) #specify coefficients of two vectors with respect to the common basis
```


```python
expr = E(c)*F(d)
expr
```




$$\displaystyle E{}^{c}F{}^{d}$$




```python
expr.replace_with_arrays(repl) #this is the component representation of $$E^c F^d$$
```




$$\displaystyle \left[\begin{matrix}5 & 6\\10 & 12\end{matrix}\right]$$



The coefficient matrix of a contraction can be obtained as well:


```python
contract = T(a,b)*S(-b,c) #lower the first slot of S^{bc} and then contract T^{ab}S_b^c
contract
```




$$\displaystyle T{}^{aV_{0}}S{}_{V_{0}}{}^{c}$$




```python
contract.replace_with_arrays(repl) #The coefficient matrix of the contraction defined above
```




$$\displaystyle \left[\begin{matrix}-4 & 17\\-28 & 49\end{matrix}\right]$$



W obtain the coefficient matrix of a rearranged tensor as follows:


```python
T(a,b).replace_with_arrays(repl) #The coefficient matrix of T^{ab}
```




$$\displaystyle \left[\begin{matrix}1 & 2\\5 & 6\end{matrix}\right]$$




```python
T(b,a).replace_with_arrays(repl) #The coefficient matrix of T^{ba} note that it is the tranpose of the coefficient matrix of T^{ab}
```




$$\displaystyle \left[\begin{matrix}1 & 5\\2 & 6\end{matrix}\right]$$



## Symmetries Of Tensors And Canonicalization

Lastly we consider the canonicalization of tensors and symmetry.
Canonicalization of a tensor expression means to bring every term in the expression into canonical form, meaning that the index labels are in alphabetic order.

Canonicalization can simplify an expression greatly, because symmetries of the individual terms can be exploited. For details on Canonicalization see [here](https://arxiv.org/pdf/1702.08114.pdf).
I wil show two examples of this.
To this end we define a (anti) symmetric tensor as follows:


```python
from sympy.tensor.tensor import TensorSymmetry
```


```python
sym2 = TensorSymmetry.fully_symmetric(2) 
asym2 = TensorSymmetry.fully_symmetric(-2) 

Sy = TensorHead('Sy', [V,V], sym2) #define a symmetric tensor of rank2
A =  TensorHead('A', [V,V], asym2) #define an anti-symmetric tensor of rank2

```


```python
expr =A(a,b)+A(b,a)
expr #the expression is not in canonical form and the anti symmetry has not been used to simplify it
```




$$\displaystyle A{}^{ab} + A{}^{ba}$$



Now we use the ``canon_bp()`` method to put the expression into canonical form. In the process the symmetry will be exploited to simplify the expression:


```python
expr.canon_bp() #put the expression into canonical form (its zero because A is anti-symmetric)
```




$$\displaystyle 0$$



The same thing also works for symmetric tensors:


```python
expr = Sy(a,b)+Sy(b,a)
expr
```




$$\displaystyle Sy{}^{ab} + Sy{}^{ba}$$




```python
expr.canon_bp() #put the expression into canonical form (its 2 Sy^{ab} because Sy is symmetric)
```




$$\displaystyle 2Sy{}^{ab}$$



More complicated symmetries can also be implemented. For example the symmetries of the Riemann curvature tensor


```python
riesym = TensorSymmetry.riemann()
R = TensorHead('R', [V,V,V,V], riesym) #define a tensor wie riemann curvature symmetries
Ric = TensorHead('Ric', [V,V]) #define a tensor wie riemann curvature symmetries
```


```python
expr = 3*R(a,b,c,d)+R(a,b,d,c) +R(b,a,c,d)-R(c,d,a,b)
expr
```




$$\displaystyle -R{}^{cdab} + 3R{}^{abcd} + R{}^{abdc} + R{}^{bacd}$$




```python
expr.canon_bp() #uses the symmetries of the riemann tensor to simplify
```




$$\displaystyle 0$$




```python
expr =R(a,b,c,d)+R(a,c,d,b)+R(a,d,b,c)
```


```python
expr.canon_bp() #the algebraic bianchi identity is not simplified (this should be 0) because it is a multi-term symmetry (and as far as i understand canonicalization only tackles single term symmetries)
```




$$\displaystyle -R{}^{acbd} + R{}^{abcd} + R{}^{adbc}$$




```python
from sympy.tensor.tensor import riemann_cyclic
```


```python
riemann_cyclic(expr) #this is a special function that can rewrite the riemann tensor in terms of cyclic combinations to exploit the multi-term symmetry
```




$$\displaystyle 0$$



The symmetries from $R$ carry over to tensors defined from it like Ricci curvature $Ric$


```python
Ric= R(-c,a,c,b)
```


```python
Ric
```




$$\displaystyle R{}_{V_{0}}{}^{aV_{0}b}$$




```python
expr = Ric + Ric._replace_indices({a:b,b:a})
```


```python
expr
```




$$\displaystyle R{}_{V_{0}}{}^{aV_{0}b} + R{}_{V_{0}}{}^{bV_{0}a}$$




```python
expr.canon_bp() #ric is symmetric 
```




$$\displaystyle 2R{}^{aV_{0}b}{}_{V_{0}}$$



## Symmetrization Of Tensors In Sympy

As i understand this is not implemented in the Tensor module of Sympy. But we can easily write a function that returns a symmetrization/anti-symmetrization as a tensor expression.
I came up with the following code (use at your own risk: not extensively tested and also probably not that fast):


```python
from sympy.combinatorics import Permutation
import math
```


```python
def symmetrizer(t,indices,anti=False):
    """(Anti)-symmetrize the factors of a tensor (expression) t which are included in the indices list"""
    sym =t
    N = len(indices)
    ind_list = [i for i in range(N)] 
    map_dict = dict(zip(ind_list,indices)) #maps number to the corresponding index object
    p = Permutation(ind_list) 
    while p.next_trotterjohnson() != None: #if all permutations have been looped stop
        p = p.next_trotterjohnson() #next permutation
        repl_dict = {indices[i] : map_dict[p.list()[i]] for i in ind_list}#replacement dict with the correct permutation
        if not anti:
            sym += t._replace_indices(repl_dict) #symmetrization
        else:
            sym += p.signature()*t._replace_indices(repl_dict) #anti-symmetrization
    return sym/(math.factorial(N))
```


```python
K = TensorHead("K",index_types =[V,V,V])
J = TensorHead("J",index_types =[V,V,V])
```


```python
symmetrizer(K(a,b,c),[a,b,c]) #Symmetrize all indices, this is K^{(abc)}
```




$$\displaystyle \left(\frac{1}{6}\right)\left(K{}^{abc} + K{}^{acb} + K{}^{bac} + K{}^{bca} + K{}^{cab} + K{}^{cba}\right)$$




```python
symmetrizer(K(a,b,c),[a,b,c],anti=True)#anti-symmetrize all indices, this is K^{[abc]}
```




$$\displaystyle \left(\frac{1}{6}\right)\left(K{}^{abc} + K{}^{bca} + K{}^{cab} + \left(-1\right)K{}^{acb} + \left(-1\right)K{}^{bac} + \left(-1\right)K{}^{cba}\right)$$




```python
symmetrizer(K(a,b,c),[a,c])#symmetrize only the first and second factor, this is K^{(a|b|c)}
```




$$\displaystyle \left(\frac{1}{2}\right)\left(K{}^{abc} + K{}^{cba}\right)$$



The function also works with arbitrary tensor expressions:


```python
expr = K(a,b,c)+J(a,b,c)
```


```python
symmetrizer(expr,[a,b,c])
```




$$ \frac{1}{6}\left( J{}^{abc} + J{}^{acb} + J{}^{bac} + J{}^{bca} + J{}^{cab} + J{}^{cba} + K{}^{abc} + K{}^{acb} + K{}^{bac} + K{}^{bca} + K{}^{cab} + K{}^{cba}\right) $$ 




```python
expr = K(a,b,c)*J(-c,d,e)
```


```python
symmetrizer(expr,[a,d])
```




$$ \left(\frac{1}{2}\right)\left(K{}^{abV_{0}}J{}_{V_{0}}{}^{de} + K{}^{dbV_{0}}J{}_{V_{0}}{}^{ae}\right)$$


