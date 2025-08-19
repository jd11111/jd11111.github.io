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

**Proposition 2 (Maximum principle for subharmonic functions):**
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

**Proposition 3:**
Let $P$ be a Perron family.
Let $u : \Omega \to (-\infty,\infty]$, $u (x) := \sup \\{ v (x) :v \in P\\}$.
Then either $u=\infty$ or $u$ is harmonic.

**Proof:**
Let $x_0 \in \Omega$ such that $u(x_0) < \infty$.
Let $(v_n)\_{n \in \mathbb{N}}$ be a sequence in $P$ such that $\lim_{n \to \infty} v_n (x) = u(x_0)$.
Without loss of generality the sequence can be chosen such that is monotone (by replacing $v_n$ with $\max \\{v_1, \dots, v_n\\}$).
Let $r \in (0, \infty)$ such that $\bar B(x_0, r) \subset \Omega$.
Let $(\bar v_n)\_{n \in \mathbb{N}}$ be the in $B(x_0, r)$ regularized sequence (which is in $P$).
By the maximums principle for $m,n \in \mathbb{N}$ with $m\geq n$ and $x \in B (x_0,r)$:
\begin{equation}
     \bar v_m (x) - \bar v_n (x) \leq \sup_{y \in \partial B(x_0,r)} (v_m (y) - v_n(y)) \leq 0
\end{equation}
Showing that $(\bar v_n)\_{n \in \mathbb{N}}$ is also monotone.
In general $v_n \leq \bar v_n $ since $v_n - \bar v_n$ is subharmonic on $B(x_0,r)$ and zero on the boundary so by the maximums principle $v_n - \bar v_n \leq 0$.
Furthermore
\begin{equation}
     v_n (x_0) \leq  \bar v_n (x_0) \leq u (x_0)  
\end{equation}
implies that $\lim_{n \to \infty} \bar v_n (x_0) = u(x_0)$.
By Harnacks convergence theorem $(\bar v_n)\_{n \in \mathbb{N}}$ converges to a harmonic function $v$ in $B(x_0,r)$. to be continued ...
