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
Let $S \subset \mathbb{R}^n$ be a non-empty bounded subset, $u \in C(S)$ and $m:= \sup_{x \in S} u(x)$.
Then either $m$ is attained in $S$ or there exists a sequence $(x_k)\_{k \in \mathbb{N}}$ in $S$ converging to a point in $\partial S$ such that $(u(x_k))\_{k \in \mathbb{N}}$ converges to $m$.

**Proof:**
Assume that $m$ is not attained.
There exists a sequence $(x_k)\_{k \in \mathbb{N}}$ in $S$ such that $(u(x_k))\_{k \in \mathbb{N}}$ converges to $m$:
Without loss of generality (by switching to a subsequence) we may assume that $(x_k)\_{k \in \mathbb{N}}$ converges in $\bar S$.
This is because $\bar S$ is compact.
Let $x_0 := \lim_{k \to \infty} x_k$.
If $x_0 \in S$ then by continuity of $u$, $(u(x_k))\_{k \in \mathbb{N}}$ converges to $u(x_0)$ and so $m = u(x_0)$ and $m$ is attained.
A contradiction.
Therefore $x_0 \in \partial S$. $\square$

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
Let $x_0 \in \Omega$ with $u(x_0) = M$. Then $u= M$, since $u$ is constant.
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
Then $x_0$ is called regular if there exists a **barrier function** $b \in C(\Omega)$ at $x_0$, that is
1. $b$ is subharmonic,
2. $\lim_{x \to x_0} b(x) = 0$,
3. For all $y \in \partial \Omega \setminus \\{ x_0\\}$: $\limsup_{\Omega \ni x \to y} b(x) <0$.

**Proposition 7:**
Let $x_0 \in \partial \Omega$ regular and
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function that is continuous in $x_0$.
Let $P_g$ the Perron family associated to $g$ and let $u$ be the Perron solution associated to $P_g$.
Then for every $\varepsilon \in (0, \infty)$ there exists $v \in P_g$ with
\begin{equation}
g(x_0)- \varepsilon =  \lim_{x \to x_0} v(x).
\end{equation}

**Proof:**
Let $b \in C(\Omega)$ be a barrier function at $x_0$.
Let $\varepsilon \in (0, \infty)$. Let $\delta \in (0, \infty)$ such that $\forall x \in B(x_0,2 \delta) \cap \partial \Omega$: $|g(x)-g(x_0)|< \varepsilon$.
Let $m := \sup_{x \in \Omega \setminus B(x_0, \delta)} b(x)$.
Then $m<0$. Since $b \leq 0$ by the maximum principle for subharmonic functions we already know $m\leq 0$.
Assume $m=0$. The function $b$ can not attain $0$, because then $b=0$ by the maximum principle contradicting item 3 in the definition of barrier.
By proposition 1 there exists a sequence $(x_n)\_{n \in \mathbb{N}}$ in $\Omega \setminus B(x_0, \delta)$ converging to a point $x \in \partial \big(\Omega \setminus B(x_0, \delta)\big)$ with $\lim_{n \to \infty} b(x_n) = 0$.
Note that $\partial \big(\Omega \setminus B(x_0, \delta)\big) \subset \bar \Omega$ which implies that $ x \in \partial \Omega$, because otherwise $b$ attains $0$ (by continuity of $b$).
Furthermore clearly $x \neq x_0$.
But then
\begin{equation}
 0  =  \lim_{n \to \infty} b(x_n) \leq  \limsup_{\Omega \ni z \to x} b(z) <0
\end{equation}
A contradiction.
Let $M := \sup_{ x\in \Omega} |g(x)|$ and $c:=-2M/m>0$.
Now define $v: \Omega \to \mathbb{R}$ by
\begin{equation}
    v(x):= g(x_0) - \varepsilon + c b(x).
\end{equation}
Then $v$ is subharmonic, because $b$ is.
Let $z \in \partial \Omega \cap B(x_0, 2 \delta)$. Then
For all $x \in \Omega \cap B(x_0, 2\delta)$:
\begin{equation}
    v(x) \leq g(z) + \underbrace{c b(x)}\_{ \leq 0} \leq g(z)
\end{equation}
and therefore $\limsup\_{\Omega \ni x \to z} v(x) \leq g(z)$.
Let $z \in \partial \Omega \setminus B(x_0, 2 \delta)$. 
Then $\Omega \cap B(z,\delta) \subset \Omega \setminus B(x_0, \delta)$ and therefore for all $x \in \Omega \cap B(z, \delta)$:
\begin{equation}
    v(x) \leq  g(x_0)  + c b(x) \leq g(x_0) + c m = g(x_0) - 2M \leq g(z),
\end{equation}
because $g(x_0) - g(z) \leq |g(x_0)| + |g(z)| \leq  2 M$ and by definition of $m$.
This implies that
\begin{equation}
    \limsup_{ \Omega \ni z \to x} v(x) \leq g(z).
\end{equation}
It follows that $v \in P_g$.

**Proposition 8 (Perron's Theorem):**
Let $x_0 \in \partial \Omega$ regular and
Let $g : \partial \Omega \to \mathbb{R}$ be a bounded function that is continuous in $x_0$.
Let $P_g$ the Perron family associated to $g$ and let $u_g$ be the Perron solution associated to $P_g$.
Then 
\begin{equation}
    \lim_{x \to x_0} u_g(x) = g(x_0).
\end{equation}

**Proof:**
Let $\varepsilon \in (0, \infty)$.
Let $v \in P_g$ with
\begin{equation}
g(x_0)- \varepsilon = \lim_{x \to x_0} v(x).
\end{equation}
Existence of $v$ is the content of proposition 7.
Consider the Perron family $P_{-g}$ associated to $-g$. The function $-g$ is also bounded and continuous in $x_0$.
Let $u_{-g}$ be the Perron solution associated to $P_{-g}$.
By proposition 7 there exists $w \in P_{-g}$ with
\begin{equation}
    - g(x_0) - \varepsilon =  \lim_{x \to x_0} w(x).
\end{equation}
Or equivalently
\begin{equation}
    g(x_0) + \varepsilon = \lim_{x \to x_0} -w(x).
\end{equation}
Since $w \in P_{-g}$ for all $ z \in \partial \Omega$:
\begin{equation}
    \limsup_{ x \to z } w(x) \leq - g(z).
\end{equation}
Let $v^\prime \in P_g$ arbitrary.
Then for all $ z \in \partial \Omega$:
\begin{equation}
     \limsup_{x \to z} (v^\prime+w) \leq g(x_0)- g(x_0) =0.
\end{equation}
By the maximum principle $v^\prime+w \leq 0$, which implies $v^\prime \leq -w$.
In particular $u_g \leq -w$.
Then by definition of $u_g$ for all $x \in \Omega$:
\begin{equation}
    v(x) \leq u_g(x)  \leq -w (x).
\end{equation}
Therefore
\begin{equation}
 g(x_0) - \varepsilon \leq   \liminf_{ x \to x_0} u_g(x) \leq g(x_0) + \varepsilon
\end{equation}
and
\begin{equation}
  g(x_0) - \varepsilon \leq   \limsup_{ x \to x_0} u_g(x) \leq g(x_0) + \varepsilon.
\end{equation}
Since this is valid for any $\varepsilon \in (0, \infty)$ we have $\lim_{x \to x_0} u_g (x) = g(x_0)$. $\square$

**Proposition 9 (the solution to the existence question in the dirichtlet problem):**
\begin{equation}
\begin{split}
    &\forall g \in C(\partial \Omega) \exists u \in C(\bar \Omega) \cap C^2(\Omega): \Delta u =0 \ \text{in} \ \Omega, \ u = g \ \text{in} \ \partial \Omega \\\\ 
&\Leftrightarrow \forall x_0 \in \partial \Omega: x_0 \ \text{is regular}. 
\end{split}
   \end{equation}

**Proof:**
$\Leftarrow$ is Perron's theorem.
