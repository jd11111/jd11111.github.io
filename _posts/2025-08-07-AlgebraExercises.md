---
layout: post
title:  "Exercises in Abstract Algebra"
date:   2025-08-07 10:00:00 +0200
categories:
---
**Exercise 1:**
Let $K$ be a finite field and $p$ its characteristic. Show that there exists $n \in \mathbb{N}$ such that $|K|= p^n$.

**Solution:**
Let $p$ be the characteristic of $K$.
Since $K$ is finite $p>0$ and so $p$ is a prime.
Let $F$ be the unique subfield of $K$ with $F \cong \mathbb{Z} /p\mathbb{Z}$.
Then $K$ is a vector space over $F$.
$K$ must be finite dimensional, because $|K|$ is finite.
Let $n$ be the ($F$) dimension of $K$.
Then $K \cong F^n$ as $F$ vector spaces and so
\begin{equation}
|K| = |F^n| =  |F|^n=  p^n.
\end{equation}

**Exercise 2:**
Let $p$ a prime, $n \in \mathbb{N}$ and $K$ a field with $|K|=p^n$.
Let $m \in \mathbb{N}$.
Show that $F:= \\{ a \in K : a^{p^m} =a \\}$ is a subfield of $K$ and that for every every $ b \in F$ there exists $a \in K$ such that $a^p= b$.

**Solution:**
By exercise $1$ and the uniqueness of the prime factor decomposition $p$ is the characteristic of $K$.
Let $\varphi : K \to K$, $\varphi (a) := a^p$.
Then $\varphi$ is a field homomorphism (called the Frobenius homomorphism), because $p$ is the characteristic of $K$.
Since $K$ is finite and $\varphi$ injective, $\varphi$ is surjective and therefore a field automorphism.
Now $F$ is the fixed field of $\varphi^m$.
This shows that $F$ is a field.
Let $b \in F$. Then $b = \varphi^m (b)= (\varphi^{m-1} (b))^p$.
And so $b = a^p$ with $a:= \varphi^{m-1} (b)$.

**Exercise 3:**
Let $p$ a prime, $n \in \mathbb{N}$ and $K  \subset \overline{\mathbb{Z}/ p \mathbb{Z}}$ with $|K|=p^n$.
Let $\alpha \in K$ such that $\alpha^{p^n-1} \in K \setminus \\{0,1\\}$.
Show that $K(\alpha)/K$ is a Galois extension. Let $G$ be the Galois group of $K(\alpha)/K$.
Show that $G$ is cyclic and that $\forall \sigma \in G$: $\sigma(\alpha)/\alpha \in K^*$.

**Solution:**
Let $f:= X^{p^n-1} - \alpha^{p^n-1} \in K[x]$.
Then $f(\alpha)=0$ and
\begin{equation}
    f = \prod_{ b \in K^*} (X-b\alpha).
\end{equation}
To show this: Let $ b \in K^\*$. Since $|K|=p^n$, $K^\*$ is cyclic with $K^\* \cong \mathbb{Z}/ (p^n-1) \mathbb{Z}$ and so $b^{p^n-1} =1$.
Therefore $f(b \alpha)=0$.
Therefore the $p^{n}-1$ distinct roots of $f$ are $b \alpha$, $b \in K^\*$ and the identity follows.
This shows that $K(\alpha)$ is the splitting field of $f$ and therefore $K(\alpha)/K$ is normal.
Since $K$ is finite it is perfect and therefore $K(\alpha)/K$ is separable.
This shows that $K(\alpha)/K$ is Galois.
Furthermore $f$ is irreducible, because if $g,h \in K[x]$ with $\deg f, \deg g \geq 1$ and $f = gh$, then there exists $S, S^\prime \subset K^\*$ both non-empty with $S \cup S^\prime = K^\*$ and $S \cap S^\prime = \varnothing$ and
\begin{equation}
    g =c \prod_{b \in S } (X-b\alpha), \quad h =c^\prime \prod_{b \in S^\prime} (X-b\alpha),
\end{equation}
where $c , c^\prime \in K^\*$.
This is because the decomposition of $f$ into irreducible factors is unique (up to reordering and associates).
Then $ \alpha^{|S|} \in K$ and $\alpha^{|S|^\prime} \in K$. But this is not possible, because: Let $j \in \\{ 1, \dots, p^{n}-2 \\}$ with  $\alpha^j \in K$.
Then ($\alpha \neq 0$ since fields are zero divisor free)
\begin{equation}
   1 =  (\alpha^j)^{p^n-1} = (\alpha^{p^n-1} )^j
\end{equation}
from which it follows that $ p^n-1 | j$ (because $\alpha^{p^n-1} \in K \setminus \\{ 0,1 \\}$). This contradicts $0<j < p^{n}-1$.
Therefore $f$ is irreducible, and $f = M_{\alpha, K}$ and so $p^n-1 =[K(\alpha): K ]= |G|$.
Define $\psi : K^\* \to G$ by $\psi(b) :=$ the unique extension of $K \to K(\alpha)$ with $\psi (b) (\alpha) = \alpha b$.
The uniqueness and existence of such an extension follows from a well known extension theorem.
Then $\psi$ is an injective group homomorphism (easily verified) and hence surjective (since $|K^\*| = p^n-1 = |G|$).
Evidently $G$ is cyclic since $K^\*$ ist and the second assertion is also easy to see.

**Exercise 4:**
Let
\begin{equation}
f:= 5 X^4 +6X^3 +7X+4581 \in \mathbb{Q} [X].
\end{equation}
Is $f$ irreducible? Is $f$ separable?

**Solution:**
Reduction Criterion (Eisenstein does not work).
Let $\pi : \mathbb{Z} \to \mathbb{Z}/2 \mathbb{Z}$ the projection and $\varphi : \mathbb{Z}[X] \to \mathbb{Z}/ 2\mathbb{Z}[X]$ the unique ring homomorphism with $\varphi|_{\mathbb{Z}} = \pi$ and $\varphi(x) =x$.
Now
\begin{equation}
    \bar f := \varphi (f) = X^4 + X + 1.
\end{equation}
Then $\deg \bar f= \deg f$ and so if $ \bar f$ is irreducible then so is $f$ by the reduction criterion.
$\bar f (0) =1$ and $\bar f(1) = 1$. Therefore $\bar f$ does not have any zeros.
Assume $\bar f = gh $ with $g, h \in \mathbb{Z}/2\mathbb{Z}[X]$ and $\deg g , \deg h \geq 1$.
Then we must have $\deg g =\deg h =2$, because $\bar f $ does not have any zeros.
The polynomials of degree 2 are (the number of them is $2^2 =4$):
\begin{equation}
    X^2, \ X^2 + X + 1, \ X^2 +1 , \ X^2 +X.
\end{equation}
All of these have a zero (and therefore can not be equal to $g$ or $h$) except $X^2 + X +1$.
Therefore $g = h = X^2 + X +1$.
\begin{equation}
   gh = (X^2 + X +1)(X^2 + X +1) = X^4 + X^3 + X^2 + X^3 + X^2 +X + X^2 + X +1
\end{equation}
And so 
\begin{equation}
gh = X^4 + 2 X^3 + 3 X^2 + 2 X +1  \neq \bar f.
\end{equation}
Therefore $\bar f$ is irreducible and so $f$ is too.

**Exercise 5:**
Let $K:= \mathbb{Q}$ and $E:= K(\sqrt{2},\sqrt{3})$.
1. Show that $E/K$ is Galois
2. Show that the Galois group $G$ of $E/K$ is isomorphic to $(\\{-1,1\\},\cdot)^2$
3. What are the subextensions of $E/K$?
4. Find $\alpha \in E$ so that $E = K(\alpha)$
5. What is the minimal polynomial of $\alpha$ over $K$/ $K(\sqrt{2})$
6. Is $K (\sqrt{2}, \sqrt{3})/ K (\sqrt{2})$ normal?

**Solution:**
**To 1.:** $E$ is the splitting field of $f:= (X^2-2)(X^2-3)$.
Therefore $E/K$ is normal.
Since $K$ is perfect and $E/K$ algebraic, $E/K$ is separable.
And so in total $E/K$ is Galois.

**To 2.:** $X^2 -2$ is irreducible over $K$ by Eisensteins criterion (with $p=2$). Therefore $[K(\sqrt{2}):K]=2$.
Now $X^2 -3 = (X+\sqrt{3})(X-\sqrt{3})$ is also irreducible over $K(\sqrt{2})$, because otherwise $\sqrt{3} \in K(\sqrt{2})$.
However if $\sqrt{3} \in K(\sqrt{2})$: Then there exist $a,b \in \mathbb{Q}$ such that
\begin{equation}
    \sqrt{3} = a + b \sqrt{2}
\end{equation}
and then (assuming $a,b \neq 0$)
\begin{equation}
    3 = a^2 +2ab \sqrt{2} +2 \Rightarrow \sqrt{2} \in \mathbb{Q}
\end{equation}
Which is a contradiction.
Therefore the minimal polynomial of $\sqrt{3}$ over $K(\sqrt{2})$ is $X^2-3$ and so in total
\begin{equation}
    [K(\sqrt{2},\sqrt{3}) :K] = [K(\sqrt{2})(\sqrt{3}) :K(\sqrt{2})]  [K(\sqrt{2}):K] = 4.
\end{equation}
Therefore $|G|=4$.
For $s \in \\{-1,1\\}^2$ let $\sigma \in G$ be the unique extension of the injection $K \to E$ with $\sigma ( \sqrt{2} ) := s_1 \sqrt{2}$ and $\sigma(\sqrt{3}):= s_2 \sqrt{3}$.
This extension exists and is unique, because of the just found minimal polynomials and a general result on extension of field homomorphisms.
The map $\\{-1,1\\}^2 \ni s \mapsto \sigma_s \in G$ is an injective group homomorphism.
This is easily verified on the basis of $E/K$ given by $(1,\sqrt{2}, \sqrt{3}, \sqrt{6})$.
The group homomorphism is also surjective, because $|G| =4 = |\\{-1,1\\}^2|$.
Therefore $G$ is isomorphic to $\\{-1,1\\}^2$.

**To 3.:** Using the fundamental theorem of Galois theory we only need to find all subgroups of $\\{-1,1\\}^2$.
The order of any subgroup must divide $4 =2 2$. Therefore the order must be one of $1,2,4$.
The subgroups are given by
\begin{equation}
H_1 := \\{(1,1) \\}, \ H_2 :=\\{-1,1\\}^2, \ H_3 := \\{(1,1) , (1,-1) \\},
\end{equation}
\begin{equation}
    H_4 := \\{(1,1), (-1,1)\\}, \ H_5 := \\{ (1,1), (-1,-1) \\}.
\end{equation}
Therefore (the non trivial) subextensions of $E/K$ are (easily verified on the above basis):
\begin{equation}
    E^{H_3} =  K(\sqrt{2}), \ E^{H_4} = K ( \sqrt{3}), \ E^{H_5} = K (\sqrt{6}).
\end{equation}

**To 4.:**
The roots of the minimal polynomial of $\sqrt{2}$ are $\sqrt{2}$ and $-\sqrt{2}$.
The roots of the minimal polynomial of $\sqrt{3}$ are $ \sqrt{3}$ and $- \sqrt{3}$.
Let $\mu :=1 $. Then
\begin{equation}
    \mu \neq 0 = \frac{\sqrt{2}- \sqrt{2}}{-\sqrt{3}- \sqrt{3}}
\end{equation}
and
\begin{equation}
    \mu \neq  \frac{ \sqrt{2} -(-\sqrt{2})}{- \sqrt{3}- \sqrt{3}} = -\frac{\sqrt{2}}{\sqrt{3}}.
\end{equation}
Let $ \alpha = \sqrt{2}+ \mu \sqrt{3}$.
Then $E= K(\alpha)$ by the primitive element theorem.

**To 5.:**
The minimal polynomial of $\alpha$ over $K$ has degree 4.
And
\begin{equation}
 3 =    (\alpha - \sqrt{2})^2= \alpha^2 - 2 \sqrt{2} \alpha + 2
\end{equation}
and so
\begin{equation}
    \alpha^2 -1 = 2 \sqrt{2} \alpha \Rightarrow (\alpha^2 - 1)^2 = 8 \alpha^2
\end{equation}
and therefore $\alpha$ is a root of
\begin{equation}
    (X^2-1)^2 - 8 X^2 \in K[X],
\end{equation}
which is the minimal polynomial, because it has degree $4$ and is normalized.
The minimal polynomial of $\alpha$ over $K(\sqrt{2})$ has degree 2.
It is given by (see above equation)
\begin{equation}
    (X- \sqrt{2})^2-3 \in K(\sqrt{2})[X].
\end{equation}
Since this polynomial has a root at $\alpha$ and is normalized.

**To 6.:**
$K(\sqrt{2}, \sqrt{3})$ is the splitting field of $X^2-3$ over $K(\sqrt{2})$ and therefore the extension is normal.
