---
layout: post
title:  "Perron's Method for Laplace's Equation"
date:   2025-08-19 10:00:00 +0200
categories:
---
Let $n \in \mathbb{N}$ and $\Omega \subset \mathbb{R}^n$ be a bounded region.

**Definition (subharmonic function)**:
$u \in C(\Omega)$ is called subharmonic if for every $x \in \Omega$ there exists $r_0 \in (0, \infty)$ such that $B(x,r_0) \subset \Omega$ and for all $r \in (0,r_0)$:
\begin{equation}
    u(x) \leq \frac{1}{n \alpha(n) r^{n-1}} \int_{\partial B(x,r)} u dS
\end{equation}

**Proposition 1:**
Let $u \in C(\Omega)$ and $m:= \sup_{x \in \Omega} u(x)$.
Then either $m$ is attained in $\Omega$ or there exists a sequence $(x_k)\_{k \in \mathbb{N}}$ in $\Omega$ converging to a point in $\partial \Omega$ such that $(u(x_k))\_{k \in \mathbb{N}}$ converges to $m$.

**Proof:**
Assume that $m$ is not attained.
There exists a sequence $(x_k)\_{k \in \mathbb{N}}$ in $\Omega$ such that $(u(x_k))\_{k \in \mathbb{N}}$ converges to $m$:
Without loss of generality (by switching to a subsequence) we may assume that $(x_k)\_{k \in \mathbb{N}}$ converges in $\bar \Omega$.
This is because $\bar \Omega$ is compact.
Let $x_0 := \lim_{k \to \infty} x_k$.
If $x_0 \in \Omega$ then by continuity of $u$, $(u(x_k))\_{k \in \mathbb{N}}$ converges to $u(x_0)$ and so $m = u(x_0)$ and $m$ is attained.
A contradiction.
Therefore $x_0 \in \partial \Omega$. $\square$

**Proposition 2 (maximum principle for subharmonic functions):**
Let $u \in C(\Omega)$ subharmonic.
Let $m:= \sup_{x \in \Omega} u(x)$.
Then:
1. If $u$ attains $m$, then $u$ is constant,
2. Let $M \in \mathbb{R}$ such that for all $x_0 \in \partial \Omega$
\begin{equation}
    \limsup_{\Omega \ni x \to x_0} u(x_0) \leq M.
\end{equation}
Then either $u<M$ or $u=M$.

**Proof:**
 By assumption (both for 1. and 2.) and the preceding proposition $m$ is finite.
Let $S:= \\{ x \in \Omega : u (x) = m\\}$. Then the usual argument shows that either $S= \varnothing$ or $S= \Omega$. This shows 1. For 2.:
Case 1: $S = \Omega$. 
Since $u$ is constant trivially $u \leq M$. 
Let $x_0 \in \Omega$ with $u(x_0) > M$. Then $u(x_0) = M$ and since $u$ is constant $u= M$.
Case 2: $S= \varnothing$, then $m \leq M$ by the previous proposition
and so $u< m \leq M$. $\square$

**Definition (harmonic regularisation of subharmonic functions):**
Let $v \in C(\Omega)$ subharmonic and $x \in \Omega$, $r \in (0, \infty)$ such that $\bar B(x,r) \subset \Omega$.
Then the unique $\bar v \in C(\Omega)\cap C^2 (B(x,r))$ with $\bar v = v$ on $\Omega \setminus B(x,r)$ and $\bar v$ harmonic in $B(x,r)$ is called the harmonic regularisation of $v$ in $B(x,r)$.

**Proposition 3:**
Let $v \in C(\Omega)$ subharmonic and $x \in \Omega$, $r \in (0, \infty)$ such that $\bar B(x,r) \subset \Omega$.
Let $\bar v$ be the harmonic regularisation of $v$ in $B(x,r)$.
Then $v \leq \bar v$ and $\bar v$ is subharmonic.

**Proof:**
To show $v \leq \bar v$: We know $ v -  \bar v = 0$ in $\Omega \setminus B(x,r)$ (in particular on $\partial B(x,r)$) and $ v -\bar v$ is subharmonic in $B(x,r)$.
Therefore by the maximum principle for subharmonic functions $v - \bar v \leq 0$ in $B(x,r)$.
To show that $\bar v$ is subharmonic:
Let $y \in \partial B(x,r)$ (for all other points of $\Omega$ subharmonicity is clear).
Let $\rho_0 \in (0, \infty)$ such that $B(y,\rho_0) \subset \Omega$ and for all $\rho \in (0, \rho_0)$:
\begin{equation}
    v(y) \leq \frac{1}{\alpha(n) n r^{n-1}} \int_{\partial B(y,\rho)} v dS.
\end{equation}
Let $\rho \in (0, \rho_0)$. Then
\begin{equation}
    \bar v (y) = v(y) \leq 
 \frac{1}{\alpha(n) n r^{n-1}} \int_{\partial B(y,\rho)} v dS
\leq  \frac{1}{\alpha(n) n r^{n-1}} \int_{\partial B(y,\rho)} \bar v dS,
\end{equation}
because $v \leq \bar v$. $\square$


**Definition (Perron family):**
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function.
Define the **Perron family** $P_g$ associated to $g$ by
\begin{equation}
P_g := \\{ v \in C(\Omega) : \ v \ \text{subbharmonic and } \forall x_0 \in \partial \Omega :  \limsup_{\Omega \ni x \to x_0} v(x_0)  \leq g(x_0)  \\}.
\end{equation}

**Proposition 4 (basic properties of Perron families):**
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function and $P_g$ the Perron family associated to $g$.
Then:
1. $P_g \neq \varnothing$,
2. $\forall x \in \Omega:  \sup_{ v \in P_g} v(x) <\infty$,
3. $\forall v_1, v_2 \in P_g: \max \\{v_1, v_2 \\} \in P_g$, 
4. $\forall v \in P_g$ the harmonic regularisation of $v$ in any ball that is precompact in $\Omega$ is in $P_g$.

**Proof:**
To 1.: $\inf_{x \in \partial \Omega} g(x))>-\infty$, because $g$ is bounded. Let $c \in (-\infty, \inf_{x \in \partial \Omega} g(x)]$, then $c \in P_g$.
To 2.: Let $v \in P_g$. Then for all $x_0 \in \partial \Omega$
\begin{equation}
    \limsup_{ \Omega \ni x \to x_0} v(x) \leq g(x_0) \leq \sup_{x \in \partial \Omega} g(x)<  \infty.
\end{equation}
Therefore by the maximum principle for subharmonic functions $ v\leq  \sup_{x \in \partial \Omega} g(x)<  \infty$.
To 3.: Easy to see.
To 4.: Follows from proposition 3 and the fact that the regularisation does not change the values of the function near $\partial \Omega$. $\square$

**Definition (Perron solution):**
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function and $P_g$ the Perron family associated to $g$.
The **Perron solution** $u: \Omega \to \mathbb{R}$ associated to $P_g$ is defined by 
\begin{equation}
    u(x) := \sup_{ v \in P_g} v(x).
\end{equation}

**Remark:**
The Perron solution is well defined by item 1 and 2 of the preceding proposition.

**Proposition 5 (motivation for the Perron solution):**
Let $g \in C(\partial \Omega)$, $P_g$ the Perron family associated to $g$ and $u_g$ the Perron solution associated to $P_g$. Let $u \in C(\bar \Omega) \cap C^2(\Omega)$ with $\Delta u =0$ on $\Omega$ and $u=g$ on $\partial \Omega$.
Then $u=u_g$ on $\Omega$.

**Proof:**
By the assumptions
$u \in P_g$. Therefore $u \leq u_g$.
On the other hand let $v\in P_g$.
Then $v-u$ is subharmonic and for all $x_0 \in \partial \Omega$:
\begin{equation}
    \limsup_{\Omega \ni x \to x_0} (v-u)(x) \leq 
 \limsup_{\Omega \ni x \to x_0}v(x) + 
 \limsup_{\Omega \ni x \to x_0}-u(x) 
\leq g(x_0) - u(x_0) = 0.
\end{equation}
Therefore by the maximum principle for subharmonic functions $v-u \leq 0$ on $\Omega$.
Therefore $v \leq u$. This shows that $u_g \leq u$ and therefore $u=u_g$. $\square$

**Proposition 6 (the Perron solution is harmonic):**
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function and $P_g$ the Perron family associated to $g$.
Let $u$ be the Perron solution associated to $P_g$.
Then $u$ is harmonic.

**Proof:**
Let $x_0 \in \Omega$ and $r \in (0, \infty)$ such that $\bar B(x_0, r) \subset \Omega$.
**Step 1:** Find a harmonic function $v$ on $B(x_0, r)$ that agrees with $u$ at $x_0$.

Let $(w_n)\_{n \in \mathbb{N}}$ be a sequence in $P_g$ such that $\lim_{n \to \infty} w_n (x_0) = u(x_0)$.
Define a new sequence $(v_n)\_{n \in \mathbb{N}}$ in $P_g$ by
\begin{equation}
v_n := \max \\{w_1, \dots, w_n\\}.
\end{equation}
Then $(v_n)\_{n \in \mathbb{N}}$ is monotone.
Furthermore for all $n \in \mathbb{N}$:
\begin{equation}
    w_n (x_0) \leq  v_n (x_0) \leq u(x_0),
\end{equation}
by definition of $w_n$ and $u$.
Therefore by the Sandwich lemma $\lim_{n \to \infty} v_n (x_0) = u(x_0)$.
Define the sequence $(\bar v_n)\_{n \in \mathbb{N}}$ in $P_g$ by $\bar v_n :=$ the harmonic regularisation of $v_n$ in $B(x_0, r)$.
By the maximums principle for harmonic functions: for $m,n \in \mathbb{N}$ with $m\geq n$ and $x \in B (x_0,r)$:
\begin{equation}
     \bar v_n (x) - \bar v_m (x) \leq \sup_{y \in \partial B(x_0,r)} (v_n (y) - v_m(y)) \leq 0.
\end{equation}
Showing that $(\bar v_n)\_{n \in \mathbb{N}}$ is also monotone.
Furthermore by proposition 3 for all $n \in \mathbb{N}$:
\begin{equation}
     v_n (x_0) \leq  \bar v_n (x_0) \leq u (x_0),
\end{equation}
which 
implies that $\lim_{n \to \infty} \bar v_n (x_0) = u(x_0)$.
By Harnacks convergence theorem $(\bar v_n)\_{n \in \mathbb{N}}$ converges to a harmonic function $v$ in $B(x_0,r)$.
We know that $v(x_0) =  u(x_0)$ and we want to argue that $v=u$ in $B(x_0,r)$, which would show that $u$ is harmonic.

**Step 2:** Show that $u=v$ on $B(x_0,r)$ and not just at $x_0$.
Let $x \in B(x_0, r)$.
Let $(h_n)\_{n \in \mathbb{N}}$ be a sequence in $P_g$ such that $\lim_{n \to \infty} h_n (x) = u(x)$.
Define a new sequence $(f_n)\_{n \in \mathbb{N}}$ in $P_g$ by
\begin{equation}
f_n := \max \\{h_1, \dots, h_n, \bar v_n\\}.
\end{equation}
Then $(f_n)\_{n \in \mathbb{N}}$ is monotone (using that $(\bar v_n)\_{n \in \mathbb{N}}$ is monotone).
Furthermore for all $n \in \mathbb{N}$:
\begin{equation}
    h_n (x) \leq  f_n (x) \leq u(x),
\end{equation}
by definition of $f_n$ and $u$.
Therefore by the Sandwich lemma $\lim_{n \to \infty} f_n (x) = u(x)$.
Define the sequence $(\bar f_n)\_{n \in \mathbb{N}}$ in $P_g$ by $\bar f_n :=$ the harmonic regularisation of $f_n$ in $B(x_0, r)$.
By the maximums principle for harmonic functions: for $m,n \in \mathbb{N}$ with $m\geq n$ and $z \in B (x_0,r)$:
\begin{equation}
     \bar f_n (z) - \bar f_m (z) \leq \sup_{y \in \partial B(x_0,r)} (f_n (y) - f_m(y)) \leq 0.
\end{equation}
Showing that $(\bar f_n)\_{n \in \mathbb{N}}$ is also monotone.
Furthermore by proposition 3 and the definition of $u$ for all $n \in \mathbb{N}$:
\begin{equation}
     f_n (x) \leq  \bar f_n (x) \leq u (x),
\end{equation}
which 
implies that $\lim_{n \to \infty} \bar f_n (x) = u(x)$.
By Harnacks convergence theorem $(\bar f_n)\_{n \in \mathbb{N}}$ converges to a harmonic function $f$ in $B(x,r)$.
By definition of $f$ we have $v \leq f$ on $B(x_0,r)$.
Now for all $n \in \mathbb{N}$ by definition of $f_n$, proposition 3 and the definition of $u$
\begin{equation}
 \bar v_n (x_0) \leq f_n(x_0) \leq  \bar f_n (x_0) \leq u(x_0).
\end{equation}
Therefore $ u(x_0) = \lim_{n \to \infty} \bar v_n (x_0)  =\lim_{n \to \infty} \bar f_n (x_0) = f(x_0)$.
Now $v-f$ is harmonic in $B(x,r)$ and $v-f \leq 0$ in $B(x,r)$.
Furthermore $(v-f)(x_0) = 0$ and therefore by the maximum principle for harmonic functions $v= f$ on $B(x,r)$.
In particular $u(x) = f(x) = v(x)$.
And so $v=u$ on $B(x,r)$ with $v$ harmonic. $\square$

**Definition (regular boundary point):**
Let $x_0 \in \partial \Omega$.
Then $x_0$ is called regular if there exists a **barrier function** $b \in C(\Omega)$ with
1. $b$ is subharmonic,
2. $\lim_{x \to x_0} b(x) = 0$,
3. For all $y \in \partial \Omega \setminus \\{ x_0\\}$: $\limsup_{\Omega \ni x \to y} b(x) <0$.

**Proposition 7:**
Let $x_0 \in \partial \Omega$ regular and
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function that is continuous in $x_0$.
Let $P_g$ the Perron family associated to $g$ and let $u$ be the Perron solution associated to $P_g$.
Then $\lim_{x \to x_0} u(x) = g(x_0)$.
