---
layout: post
title:  "Differentation under the Integral Sign for PDEs"
date:   2025-08-13 10:00:00 +0200
categories:
---
**Proposition 1:**
Let $(X,d)$ a metric space and $(Y, \mathscr{A} , \mu)$ a measure space.
Let $f : X \times Y \to \mathbb{R}$ such that
1. $\forall x \in X: f(x , \bullet) \in L^1 (\mu)$,
2. $\forall y \in Y : f(\bullet,  y)$ is continuous,
3. $\forall x \in X$ exists an open neighborhood $V$ of $x$ and $\exists g \in L^1(\mu)$ such that $\forall (x^ \prime,y) \in V \times Y$: $\|f(x,y)\| \leq g(y)$.

Then $u: U \to \mathbb{R}$, $u(x) := \int f(x,\bullet) d \mu$ is continuous.

**Proof:**
Let $x \in X$. Let $V$ an open neighborhood of $x$ and $g \in L^1(\mu)$ such that property 3 holds.
Let $(x_n)_{n \in \mathbb{N}}$ a sequence in $X$ converging to $x$.
Without loss of generality we may assume that the sequence takes values in $V$.
Then for all $n \in \mathbb{N}$ and $y \in Y$:
\begin{equation}
|f(x_n,y) | \leq g (y).
\end{equation}
Therefore Lebesgue's theorem of dominated convergence concludes. $\square$

**Proposition 2:**
Let $m,k \in \mathbb{N}$, $U \subset \mathbb{R}^m$ open and $(Y, \mathscr{A} , \mu)$ a measure space.
Let $f : U \times Y \to \mathbb{R}$ such that
1. $\forall x \in U: f(x , \bullet) \in L^1 (\mu)$,
2. $\forall y \in Y : f(\bullet,  y) \in C^1 (U)$,
3. $\forall x \in U$ exists an open neighborhood $V$ of $x$ and $\exists g \in L^1(\mu)$ such that $\forall (x^ \prime,y) \in V \times Y$: $\\|\nabla (f(\bullet,y))(x^\prime)\\| \leq g(y)$.

Then $u: U \to \mathbb{R}$, $u(x) := \int f(x,\bullet) d \mu$ satisfies $u \in C^1 (U)$ and for all $j \in \\{1,\dots,m \\}$ and $x \in U$:
\begin{equation}
   \partial_j u  (x) = \int \partial_j (f(\bullet,y))(x) d \mu (y).
\end{equation}

**Proof:**
Let $x \in U$.
Let $V$ an open neighborhood of $x$ and $g \in L^1(\mu)$ satisfying property 3.
Without loss of generality we may assume that $V$ is convex.
Let $(h_n)\_{n \in \mathbb{N}}$ a sequence in $\mathbb{R} \setminus \\{0\\}$ converging to $0$.
Without loss of generality we may assume that $\forall n \in \mathbb{N}$: $x+h_n e_j \in V$.
Then for all $n \in \mathbb{N}$:
\begin{equation}
    \frac{u(x+ h_n e_j) - u(x)}{h_n} = \int \frac{f(x +h_n e_j,y) - f(x,y)}{h_n} d\mu (y).
\end{equation}
Using a corollary to the mean value theorem we obtain for all $y \in Y$ and $n \in \mathbb{N}$:
\begin{equation}
     \bigg|\frac{f(x +h_n e_j,y) - f(x,y)}{h_n}\bigg| \leq \sup_{ x^\prime \in V} \\| \nabla (f(\bullet,y))(x^\prime)\\| \leq g (y).
\end{equation}
Therefore Lebesgue's theorem of dominated convergence can be applied to conclude that
$u$ is partially differentiable at $x$ in the direction $j$ and that
\begin{equation}
    \partial_j u(x) =  \int \partial_j(f(\bullet,y))(x) d\mu (y).
\end{equation}
Proposition 1 concludes that $\partial_j u$ is continuous. $\square$

**Proposition 3:** Let $m,k \in \mathbb{N}$, $h \in C\_c^k (\mathbb{R}^m)$ and $\Phi \in L^1\_{\mathrm{loc}} (\mathbb{R}^m)$. Let $u: \mathbb{R}^m \to \mathbb{R}$,
\begin{equation}
    u(x):= \int\_{ \mathbb{R}^m} h(y) \Phi(x-y) dy.
\end{equation}
Then $u \in C^k(\mathbb{R}^m)$ and for all $\alpha \in \mathbb{N}^n$ with $|\alpha|\leq k$ and $x \in \mathbb{R}^m$:
\begin{equation}
     D^\alpha u(x)= \int\_{ \mathbb{R}^m} D^\alpha h(y) \Phi(x-y) dy.
\end{equation}
**Proof:**
Assume $k=1$. The general statement follows by repeated application.
By the translation and inversion invariance of the Lebesgue measure for all $x \in \mathbb{R}^m$:
\begin{equation}
    u(x) =  \int\_{ \mathbb{R}^m} h(y) \Phi(x-y) dy = \int_{\mathbb{R}^n} h(x-y) \Phi (y) dy.
\end{equation}
Let $f : \mathbb{R}^m \times \mathbb{R}^m \to \mathbb{R}$ $f(x,y) := h(x-y) \Phi(y)$.
Evidently $f$ satisfies assumption 1 and 2 of proposition 2.
Let $x \in \mathbb{R}^n$.
Let $R \in (0, \infty)$ such that the support of $h$ is contained in $B(0,R)$.
Let $\varepsilon \in (0, \infty)$.
Let $x^\prime \in B(x,\varepsilon)$. Then the support of $h(x^\prime - \bullet)$ is contained in $\bar B(x,R+\varepsilon)$.
Since for $y \in \mathbb{R}^n$ with $\\|x^\prime - y \\|< R$:
\begin{equation}
    \\| y-x \\| = \\| y-x^\prime + x^\prime - x\\| < R + \varepsilon.
\end{equation}
Let $\chi$ be the characteristic function of $\bar B(x, R+ \varepsilon)$.
Then for all $y \in \mathbb{R}^n$:
\begin{equation}
    \\| (\nabla f (\bullet,y))(x^\prime)\\| \leq \sup_{z \in \mathbb{R}^n} \\|\nabla h (z)\||  | \chi(y) \Phi(y)|.
\end{equation}
Therefore condition 3 of proposition 2 is fullfilled and so proposition 2 concludes the proof. $\square$
