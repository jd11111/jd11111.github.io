---
layout: post
title:  "Power-Series In Banach Spaces And Algebras"
date:   2023-11-26 11:13:45 +0200
categories:
---

This post is a review of some important results on series and power series in Banach spaces and algebras.
Some knowledge about Banach spaces / algebras is presumed.

The following topics are covered:

- [Series In Banach Spaces](#series-in-banach-spaces)
- [Power Series In Banach Spaces ](#power-series-in-banach-spaces)
- [Power Series In Banach Algebras](#power-series-in-banach-algebras)

# Series In Banach Spaces

Let $X$ be a Banach space and let $ (x_i)_{i \in \mathbb{N}} $ be a sequence in $X$.
Define the sequence $ (s_n)_{n \in \mathbb{N}} $ by
$$
\begin{equation}
 s_n = \sum_{i=1}^n  x_i.
\end{equation}
 $$
If $ (s_n)_{n \in \mathbb{N}} $ is convergent the limit is denoted by $ \sum_{i=1}^\infty x_i $.

**Proposition:**
If $ (s_n)_{n \in \mathbb{N}} $ converges, then $ \lim_{i \to \infty} x_i =0 $.

**Proof:** 
Let $\varepsilon >0$.
Since convergent sequences are Cauchy there is a $N \in \mathbb{N}$ so that 
$$
\begin{equation}
 \| s_n - s_m \| < \varepsilon
\end{equation}
$$
for all $n,m >N$.
In particular with $m = n-1$: 
$$
\begin{equation}
\| x_n \| = \| s_n -s_{n-1} \| < \varepsilon
\end{equation}
$$
for all $n > N+1$.

**Definition:**
The sequence $(s_n)_{n \in \mathbb{N}}$ is called **absolutely convergent** if $\sum_{i=1}^\infty \| x_i \|< \infty$.

**Proposition:** Assume that  $(s_n)_{n \in \mathbb{N}}$ converges absolutely. Then $(s_n)_{n \in \mathbb{N}}$ converges and the sequence $(\tilde{s}_n)_{n \in \mathbb{N}}$
defined by $\tilde{s}_n = \sum_{i}^n x_{\pi (i)}$ 
 converges to the same limit for every bijective map $\pi : \mathbb{N} \to \mathbb{N}$.

**Proof:** 
Let $m,n \in \mathbb{N}$.
Set $N = \min \{m,n\}$ and $M = \max \{m,n \}$. Then
$$
\begin{equation}
\|s_m -s_n \| \leq \sum_{i=N+1}^M \| x_i \| \leq \sum_{i=N+1}^\infty \| x_i \|  \to 0 \quad  (N \to \infty).
\end{equation}
$$
So $(s_n)_{n \in \mathbb{N}}$ is Cauchy and therefore convergent since $X$ is complete. Let $s$ be limit. 
Now let $\pi : \mathbb{N} \to \mathbb{N}$ be bijective. Let $\varepsilon >0$. Since convergent sequences are Cauchy there exist an $N \in \mathbb{N}$
with 
$$
\begin{equation}
\sum_{i=n}^m \| x_i\| <\varepsilon
\end{equation}
$$
for all $m\geq n \geq N$.
Let $k \in \mathbb{N}$ be so that $\{1, \dots, N\} \subset \{ \pi(1), \pi(2) \dots, \pi(k) \}$. Note that $k\geq N$.
Then for any $n \in \mathbb{N}$ with $n>k$:
$$
\begin{equation}
\|  \tilde{s}_n - s_n \| \leq \sum_{ i = N+1 }^n  \| x_i\| < \varepsilon.
\end{equation}
$$
And so
$$
\begin{equation}
\| \tilde{s}_n -s \| = \| \tilde{s}_n - s_n + s_n -s \|  \leq \|  \tilde{s}_n -s_n \|  + \| s_n -s \| \to 0 \quad (n \to \infty).
\end{equation}
$$

**Proposition**:
Let $r = \limsup_{n \to \infty} \|x_n\|^{1/n}  $. Then 
- if $r<1$, then $(s_n)_{n \in \mathbb{N}}$ converges absolutely,
- if $r>1$,  then $(s_n)_{n \in \mathbb{N}}$ is divergent.

This is the so called **root test**.

**Proof:**
Assume $r<1$. By definition $r$ is the supremum of all cluster points of the sequence.
Now choose $\varepsilon>0$ so small, so that $\beta := r+ \varepsilon <1$. Then $\beta$ is strictly larger than any cluster point of the sequence and therefore there exist an $N \in \mathbb{N}$ so that $\|x_n\| < \beta ^n$ for all $n \geq N$. Since $\sum_{k=1}^\infty \beta^k <\infty$ it follows for $M \in \mathbb{N}$ with $M>N$ that
$$
\begin{equation}
\sum_{n=1}^M \| x_n \| \leq
\sum_{n=1}^N \| x_n \|  + \sum_{n= N+1}^M   \beta^n \leq  \sum_{n=1}^N \| x_n \|  + \sum_{n= N+1}^\infty   \beta^n <\infty. 
\end{equation}
$$
And therefore $(s_n)_{n \in \mathbb{N}}$ converges absolutely.
If $r>1$, then there is a $\varepsilon>0$ with $r-\varepsilon >1$. Since $r$ is the supremum of cluster points, this means that there is a cluster point $c$ with 
$c \geq r- \varepsilon >1$. But this means that there is a subsequence $ (\|x_{n_k}\|^{1/n_k})_{k \in \mathbb{N}}$ that converges to $c$.
But then $(x_{n})_{n \in \mathbb{N}}$ is not a null sequence contradicting the convergence of $(s_n)_{n \in \mathbb{N}}$.

# Power Series In Banach Spaces

For $a \in \mathbb{C}$ and $r \in [0, \infty]$. Define
$$
\begin{equation}
D(a,r) := \{ z \in \mathbb{C} : | z-a| <r\}.
\end{equation}
$$

**Proposition:** Let $X$ be a complex Banach space and $(c_n)_{n \in \mathbb{N}}$ a sequence in $X$. Then there exist a unique $R \in [0, \infty]$, called the **radius of convergence**, so that
$$
\begin{equation}
\sum_{n = 0}^\infty c_n z^n
\end{equation}
$$
converges absolutely for all $z \in D(0,R)$ and uniformly (in $z$) on $\bar D(0,r)$ for all $r<R$, but diverges for all $z \notin \bar D (0,R)$.
Furthermore
$$
\begin{equation}
R = \frac{1}{\limsup_{n \to \infty} \|c_n\|^{1/n}} = \liminf_{n \to \infty} \|c_n\|^{-1/n}.
\end{equation}
$$
**Proof:**
Define a sequence $(x_n)_{n \in \mathbb{N}}$ in $X$ by setting $x_n = c_n z^n$.
Then 
$$
\begin{equation}
\limsup_{n \to \infty} \|x_n \|^{1/n} =  |z| \limsup_{n \to \infty } \|c_n\|^{1/n}  = \frac{|z|}{R}
\end{equation}
$$
which is $<1$ if $z \in D(0,R)$ and $>1$ if $z \notin \bar D (0,R)$. So the part about the absolute convergence / divergence and the uniqueness of $R$ follow from the root test.
It is left to show the assertion on the uniform convergence.
Let $r<R$ and $\varepsilon >0$ so that $r+ \varepsilon< R$. Then by the definition of the $\liminf$ there is a $M \in \mathbb{N}$ so that
$r + \varepsilon \leq \|c_n\|^{-1/n}$ for all $n \geq M$.
 Then for $N>M$:
$$
\begin{equation}
\sup_{z \in \bar D(0,r)} \| \sum_{n=0}^\infty c_n z^n - \sum_{n = 0}^N c_n z^n \| 
= \sup_{z \in \bar D(0,r)} \|  \sum_{n=N+1}^\infty c_n z^n \|   \leq  \sup_{z \in \bar D(0,r)}  \sum_{n=N+1}^\infty  |z|^n \|c_n\|
\leq    \sum_{n=N+1}^\infty \bigg( \frac{r}{r+ \varepsilon} \bigg)^n \to 0 \quad (N \to \infty).
\end{equation}
$$

# Power Series In Banach Algebras

Let $A$ be a (complex, unital) Banach Algebra and $(c_n)_{n \in \mathbb{N}}$ a sequence of complex numbers. 
Furthermore let 
$$
\begin{equation}
R = \frac{1}{\limsup_{n \to \infty} |c_n|^{1/n}} = \liminf_{n \to \infty} |c_n|^{-1/n}
\end{equation}
$$
and $r(a) = \limsup_{n \to \infty } \|a^n \|^{1/n} $ be the spectral radius of $a \in A$ (note that $r(a) \leq \|a\|$).

**Proposition**:
The series 
$$
\begin{equation}
\sum_{n=0}^\infty c_n a^n
\end{equation}
$$
converges absolutely for all $a \in A$ with $r (a) < R$. Furthermore the convergence is uniform (in $a$) on $\bar B(0,r)$ (ball with radius $r$ in $A$) for any $r<R$.

**Proof:**
Define a sequence $(x_n)_{n \in \mathbb{N}}$ in $A$ by $x_n = c_n a^n$.
Then
$$
\begin{equation}
\limsup_{n \to \infty } \|x_n\|^{1/n} \leq \limsup_{n \to \infty }  |c_n|^{1/n} \|a^n\|^{1/n} \leq \big( \limsup_{n \to \infty }  |c_n|^{1/n} \big) \big( \limsup_{n \to \infty}\|a^n\|^{1/n}  \big) = \frac{r(a)}{R}<1.
\end{equation}
$$
The absolute convergence follows from the above using the root test.
The assertion about the uniform convergence follows almost exactly as in the preceding proposition with $a$ taking the place of $z$ and $B(0,a)$ taking the place of $D(0,r)$ and further using that $\|a^n\| \leq \|a\|^n \leq r^n$ for all $a$ inside of the ball.

**Remark:**
It is important to note that there is no divergence assertion in the above proposition. This is because it is possible that $0 \neq a \in A $ but $a^2=0$. Therefore it is possible that the above series converges for $a \in A$ with $\|a\| >R$.
