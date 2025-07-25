---
layout: post
title:  "Curvature and Derivative On Riemannian Manifolds With Sympy Tensor"
date:   2023-06-28 11:14:45 +0200
categories:
---
In this post i will show you how to use the [Sympy Tensor](https://docs.sympy.org/latest/modules/tensor/index.html) module to calculate the covariant derivative of an arbitrary tensor field on a Riemannian manifold.
I also show how to calculate the Christoffel symbols and the different curvature quantities (Riemann tensor, Ricci tensor, scalar curvature). If you want to learn more about the Sympy Tensor module, i also wrote a post describing its features [here](https://jd11111.github.io/2023/06/23/SympyTensor.html).

The following topics are covered:

- [General Code](#general-code)
    - [Natural Derivative and Christoffel Symbols](#natural-derivative-and-christoffel-symbols)
    - [Covariant Derivative](#covariant-derivative)
    - [Riemann Curvature](#riemann-curvature)
- [Example: The 2 Sphere](#example-the-2-sphere)
    - [Christoffel Symbols](#calculation-of-the-christoffel-symbols)
    - [Differential Operators](#differential-operators-in-spherical-coordinates)
    - [Curvature of the Sphere](#calculating-the-curvature-of-the-sphere)



# General Code

In this section i will show you and briefly describe the code to compute curvature and the covariant derivative.

```python
from sympy.tensor.tensor import TensorIndexType, TensorHead, TensorSymmetry, tensor_indices 
from sympy.tensor.toperators import PartialDerivative
from sympy import symbols
from sympy.combinatorics import Permutation
import math
import sympy
```


```python
V= TensorIndexType('V', dummy_name='l',metric_name="g")
a, b,c,d,e,h,i,j  = tensor_indices('a, b,c,d,e,h,i,j', V) #create two indices associated to V (the same as the abcde etc above)

A = TensorHead("A", [V])
B = TensorHead("B", [V,V])
C = TensorHead("C", [V])

x = TensorHead("x", [V]) # storing the variables to derive by in the natural derivative

sym = TensorSymmetry.fully_symmetric(2) #metric tensor is symmetric 
g = TensorHead("g", [V,V],sym) #metric tensor 

rie_sym = TensorSymmetry.riemann() #symmetry of Riemann curvature
R = TensorHead("R",[V,V,V,V],rie_sym)

Csym = TensorSymmetry.direct_product(1,2) #symmetry of Christoffel symbols
G = TensorHead(r"\Gamma",[V,V,V],Csym) 
```

## Natural Derivative And Christoffel Symbols

Firstly define the natural derivative:


```python
def ord_der(new_ind,expr):
    return PartialDerivative(expr,x(new_ind))
```

The Christoffel symbols are obtained from the metric and the natural derivative by the following formula:


```python
ch_syms = g(c,d)*(ord_der(a,g(-b,-d))+ord_der(b,g(-a,-d)) -ord_der(d,g(-a,-b)))/2
```


```python
ch_syms
```



\begin{equation}
\displaystyle \left(\frac{1}{2}\right)g{}^{cl\_{0}}\left(\frac{\partial}{\partial {x{}^{a}}}{g{}\_{bl\_{0}}} + \frac{\partial}{\partial {x{}^{b}}}{g{}\_{al\_{0}}} + \left(-1\right)\frac{\partial}{\partial {x{}^{l\_{0}}}}{g{}\_{ab}}\right)
\end{equation}


## Covariant Derivative

Define the covariant derivative from the well known formula in terms of Christoffel symbols:


```python
def cov_der(new_ind,expr):
    inds = expr.get_free_indices()
    rexpr = ord_der(new_ind,expr)
    dummy = tensor_indices("d_asdf", V)
    for t_ind in inds:
        if t_ind.is_up:
            contract_expr = expr.substitute_indices({t_ind:dummy,dummy:None})
            rexpr += G(t_ind,-new_ind,-dummy)*contract_expr
        else:
            contract_expr = expr.substitute_indices({-t_ind:-dummy,dummy:None})
            rexpr += -G(dummy,-new_ind,t_ind)*contract_expr
    return rexpr
```

Time to check if it works in some special cases:


```python
E = TensorHead("E",[V,V,V])
T = TensorHead("T",[V])
```


```python
cov_der(a,E(a,b,-c))
```



\begin{equation}
\displaystyle -\Gamma{}^{l\_{0}}{}\_{l\_{1}c}E{}^{l\_{1}b}{}\_{l\_{0}} + \Gamma{}^{b}{}\_{l\_{0}l\_{1}}E{}^{l\_{0}l\_{1}}{}\_{c} + \Gamma{}^{l\_{0}}{}\_{l\_{0}l\_{1}}E{}^{l\_{1}b}{}\_{c} + \frac{\partial}{\partial {x{}^{l\_{0}}}}{E{}^{l\_{0}b}{}\_{c}}
\end{equation}



Divergence of a vector field:


```python
divA = cov_der(i,A(i))
```


```python
divA
```



\begin{equation}
\displaystyle \Gamma{}^{l\_{0}}{}\_{l\_{0}l\_{1}}A{}^{l\_{1}} + \frac{\partial}{\partial {x{}^{l\_{0}}}}{A{}^{l\_{0}}}
\end{equation}



## Riemann Curvature


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

Define the Riemann curvature tensor $R^{a}{}\_{bcd}$ from the well known expression in terms of Christoffel symbols 


```python
Rie = -2*symmetrizer(ord_der(a,G(d,-b,-c)),[-a,-b],anti=True) \
    + 2*symmetrizer(G(e,-c,-a)*G(d,-b,-e),[-a,-b],anti=True)
```


```python
Rie
```



\begin{equation}
\displaystyle -\Gamma{}^{l\_{0}}{}\_{cb}\Gamma{}^{d}{}\_{al\_{0}} - \left(\frac{\partial}{\partial {x{}^{a}}}{\Gamma{}^{d}{}\_{bc}} + \left(-1\right)\frac{\partial}{\partial {x{}^{b}}}{\Gamma{}^{d}{}\_{ac}}\right) + \Gamma{}^{l\_{0}}{}\_{ca}\Gamma{}^{d}{}\_{bl\_{0}}
\end{equation}




```python
Rie.free_indices
```




    [d, -b, -c, -a]



# Example: The 2 Sphere


```python
from sympy import diag
theta, phi,r = symbols(r"\theta \varphi r")
```

In this example the first coordinate will be $\theta$ (polar angle) and the second $\varphi$ (azimuthal angle). The radius $r$ of the sphere is a constant.

Inserting the coordinate matrix of the metric tensor


```python
repl = {
    V : diag(r**2,r**2*sympy.sin(theta)**2),
    g(-e,-j) : diag(r**2,r**2*sympy.sin(theta)**2),
    x(i) : [theta, phi]
        }
```

The components $g\_{\mu \nu}$ of the metric $g$ are:


```python
g(-e,-j).replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \left[\begin{matrix}r^{2} & 0\\\\0 & r^{2} \sin^{2}{\left(\theta \right)}\end{matrix}\right]
\end{equation}



## Calculation of the Christoffel-Symbols


```python
ch_syms
```



\begin{equation}
\displaystyle \left(\frac{1}{2}\right)g{}^{cl\_{0}}\left(\frac{\partial}{\partial {x{}^{a}}}{g{}\_{bl\_{0}}} + \frac{\partial}{\partial {x{}^{b}}}{g{}\_{al\_{0}}} + \left(-1\right)\frac{\partial}{\partial {x{}^{l\_{0}}}}{g{}\_{ab}}\right)
\end{equation}




```python
G_coord = ch_syms.replace_with_arrays(repl)
```


```python
repl.update({G(e,-j,-h): G_coord})
```

The Christoffel Symbols $\Gamma^\mu\_{\nu \rho}$ are:


```python
G(d,-a,-b).replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \left[\begin{matrix}\left[\begin{matrix}0 & 0\\\\0 & - \sin{\left(\theta \right)} \cos{\left(\theta \right)}\end{matrix}\right] & \left[\begin{matrix}0 & \frac{\cos{\left(\theta \right)}}{\sin{\left(\theta \right)}}\\\\\frac{\cos{\left(\theta \right)}}{\sin{\left(\theta \right)}} & 0\end{matrix}\right]\end{matrix}\right]
\end{equation}



## Differential Operators In Spherical Coordinates


```python
df = TensorHead("df",[V])
```


```python
fun = sympy.Function('f')(theta,phi)
```

### The Gradient In Spherical Coordinates


```python
repl.update({df(-i) : [sympy.Derivative(fun,theta),sympy.Derivative(fun,phi)]})
```

The components $(\mathrm{grad}f)_\mu$ of the gradient are:


```python
df(i).replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \left[\begin{matrix}\frac{\frac{\partial}{\partial \theta} f{\left(\theta,\varphi \right)}}{r^{2}} & \frac{\frac{\partial}{\partial \varphi} f{\left(\theta,\varphi \right)}}{r^{2} \sin^{2}{\left(\theta \right)}}\end{matrix}\right]
\end{equation}



### The Laplacian


```python
laplace = cov_der(i,df(i))
```

The laplacian $\Delta f$ is:


```python
laplace.replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \frac{\frac{\partial^{2}}{\partial \theta^{2}} f{\left(\theta,\varphi \right)}}{r^{2}} + \frac{\cos{\left(\theta \right)} \frac{\partial}{\partial \theta} f{\left(\theta,\varphi \right)}}{r^{2} \sin{\left(\theta \right)}} + \frac{\frac{\partial^{2}}{\partial \varphi^{2}} f{\left(\theta,\varphi \right)}}{r^{2} \sin^{2}{\left(\theta \right)}}
\end{equation}



### The Divergence Of A Vectorfield


```python
Aphi= sympy.Function(r'A^\varphi')(theta,phi)
Atheta = sympy.Function(r'A^\theta')(theta,phi)
repl.update({A(i):[Atheta,Aphi]})
```

So that the vector field is $A^i = A^\theta \frac{\partial}{\partial \theta} + A^\varphi \frac{\partial}{\partial \varphi} $


```python
divA
```



\begin{equation}
\displaystyle \Gamma{}^{l\_{0}}{}\_{l\_{0}l\_{1}}A{}^{l\_{1}} + \frac{\partial}{\partial {x{}^{l\_{0}}}}{A{}^{l\_{0}}}
\end{equation}



The divergence $\mathrm{div}A$ is:


```python
divA.replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \frac{A^{\theta}{\left(\theta,\varphi \right)} \cos{\left(\theta \right)}}{\sin{\left(\theta \right)}} + \frac{\partial}{\partial \theta} A^{\theta}{\left(\theta,\varphi \right)} + \frac{\partial}{\partial \varphi} A^{\varphi}{\left(\theta,\varphi \right)}
\end{equation}



## Calculating The Curvature Of The Sphere

 Riemann Curvature:


```python
Rie
```



\begin{equation}
\displaystyle -\Gamma{}^{l\_{0}}{}\_{cb}\Gamma{}^{d}{}\_{al\_{0}} - \left(\frac{\partial}{\partial {x{}^{a}}}{\Gamma{}^{d}{}\_{bc}} + \left(-1\right)\frac{\partial}{\partial {x{}^{b}}}{\Gamma{}^{d}{}\_{ac}}\right) + \Gamma{}^{l\_{0}}{}\_{ca}\Gamma{}^{d}{}\_{bl\_{0}}
\end{equation}




```python
Rie_coord = Rie.replace_with_arrays(repl,[-a,-b,-c,-d])
```

The components $R\_{\mu \nu \rho \sigma}$ of the Riemann curvature tensor are:


```python
Rie_coord
```



\begin{equation}
\displaystyle \left[\begin{matrix}\left[\begin{matrix}0 & 0\\\\0 & 0\end{matrix}\right] & \left[\begin{matrix}0 & r^{2} \sin^{2}{\left(\theta \right)}\\\\- r^{2} \sin^{2}{\left(\theta \right)} & 0\end{matrix}\right]\\\\\left[\begin{matrix}0 & - r^{2} \sin^{2}{\left(\theta \right)}\\\\r^{2} \sin^{2}{\left(\theta \right)} & 0\end{matrix}\right] & \left[\begin{matrix}0 & 0\\\\0 & 0\end{matrix}\right]\end{matrix}\right]
\end{equation}




```python
repl.update({R(-a,-b,-c,-d): Rie_coord})
```

The components $R^\mu{}\_{\nu \rho \sigma}$ of the Riemann curvature tensor are:


```python
R(a,-b,-c,-d).replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \left[\begin{matrix}\left[\begin{matrix}0 & 0\\\\0 & 0\end{matrix}\right] & \left[\begin{matrix}0 & \sin^{2}{\left(\theta \right)}\\\\- \sin^{2}{\left(\theta \right)} & 0\end{matrix}\right]\\\\\left[\begin{matrix}0 & -1\\\\1 & 0\end{matrix}\right] & \left[\begin{matrix}0 & 0\\\\0 & 0\end{matrix}\right]\end{matrix}\right]
\end{equation}



Ricci Curvature:


```python
Ric = R(e,-a,-e,-b)
```


```python
Ric
```



\begin{equation}
\displaystyle R{}^{l\_{0}}{}\_{al\_{0}b}
\end{equation}



The components $\mathrm{Ric}\_{\mu \nu}$ of the Ricci Tensor are:


```python
Ric.replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \left[\begin{matrix}1 & 0\\\\0 & \sin^{2}{\left(\theta \right)}\end{matrix}\right]
\end{equation}



Scalar Curvature:


```python
S = Ric._replace_indices({-a:a,-b:-a})
```


```python
S
```



\begin{equation}
\displaystyle R{}^{l\_{0}a}{}\_{l\_{0}a}
\end{equation}



The scalar curvature is:


```python
S.replace_with_arrays(repl)
```



\begin{equation}
\displaystyle \frac{2}{r^{2}}
\end{equation}


