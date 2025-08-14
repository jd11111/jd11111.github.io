---
layout: post
title:  "Differentation under the Integral Sign for PDEs"
date:   2025-08-13 10:00:00 +0200
categories:
---
**Proposition 1:** Let $m \in \mathbb{N}$, $f \in C_c (\mathbb{R}^m)$ and $\Phi \in L^1_{\mathrm{loc}} (\mathbb{R}^m)$.
Let $u: \mathbb{R}^m \to \mathbb{R}$,
\begin{equation}
    u(x):= \int\_{ \mathbb{R}^m} f(y) \Phi(x-y) dy.
\end{equation}
Then $u$ is continuous.

**Proof:**
$u$ is well defined, because $\Phi$ is locally integrable.
By the inversion and translation invariance of the Lebesgue measure:
For all $x \in \mathbb{R}^m$:
\begin{equation}
    u(x)= \int\_{ \mathbb{R}^m} f(x-y) \Phi(y) dy.
\end{equation}
Let $x_0 \in \mathbb{R}^m$ and $(x_n)\_{n \in \mathbb{N}}$ a sequence in $\mathbb{R}^m$ converging to $x_0$.
Let $M:= \sup\_{n\in \mathbb{N}} \\| x_n \\|$. Then $M<\infty$, because convergent sequences are bounded.
Let $R \in (0, \infty)$ such that the support of $f$ is contained in $B(0,R)$ and let $K:= \bar B(0,R+M)$.
Let $n \in \mathbb{N}$ and $y \in \mathbb{R}^m$ so that $f(x_n-y)\neq 0$.
Then $|x_n-y| < R$ and so
\begin{equation}
    |y| = |-y| = |x_n-y + x_n| \leq |x_n-y| + |x_n | \leq R+M.
\end{equation}
Therefore $y \in K$. 
In total for all $ n \in \mathbb{N}$:
\begin{equation}
    u(x_n) = \int_K \Phi(y) f(x_n-y) dy.
\end{equation}
The integrand converges pointwise to $K \ni y \mapsto \Phi(y) f(x_0-y)$, because $f$ is continuous.
The absolute value of the integrand has the integrable majorant $K \ni y \mapsto |\Phi(y)| \sup\_{z \in \mathbb{R}^m} |f(z)|$. 
Therefore Lebesgues theorem of dominated convergence implies that $\lim\_{n\to \infty} u(x_n) = u(x_0)$. $\square$


**Proposition 2:** Let $m,k \in \mathbb{N}$, $f \in C_c^k (\mathbb{R}^m)$ and $\Phi \in L^1_{\mathrm{loc}} (\mathbb{R}^m)$.
Let $u: \mathbb{R}^m \to \mathbb{R}$,
\begin{equation}
    u(x):= \int\_{ \mathbb{R}^m} f(y) \Phi(x-y) dy.
\end{equation}
Then $u \in C^k(\mathbb{R}^m)$ and for all $\alpha \in \mathbb{N}^n$ with $|\alpha|\leq k$ and $x \in \mathbb{R}^m$:
\begin{equation}
     D^\alpha u(x)= \int\_{ \mathbb{R}^m} D^\alpha f(y) \Phi(x-y) dy.
\end{equation}
**Proof:**
Assume $k=1$. The general statement follows by repeated application.
Let $j \in \\{1,\dots,n \\}$ and $x \in \mathbb{R}^m$.
Let $(h_n)\_{n \in \mathbb{N}}$ a sequence in $\mathbb{R}^m \setminus \\{0\\}$ converging to $0$.
Let $M:= \sup\_{n\in \mathbb{N}} \\| h_n \\|$. Then $M<\infty$, because convergent sequences are bounded.
Let $R \in (0, \infty)$ such that the support of $f$ is contained in $B(0,R)$.
Let $K:= \bar B(x, R+ M)$.
Let $n \in \mathbb{N}$ and $y \in \mathbb{R}^m$ such that $f(x-y + h_ne_j ) \neq 0$.
Then $|x-y + h_n e_j|<R$
and therefore
\begin{equation}
    |y-x| = |x-y| \leq |x-y +h_n e_j - h_n e_j| \leq |x-y + h_n e_j| + |h_n| \leq R +M,
\end{equation}
that is $y \in K$.
This implies that for all $n \in \mathbb{N}$:
\begin{equation}
    \frac{u(x+ h_n e_j) - u(x)}{h_n} = \int_K \Phi(y) \frac{f(x-y +h_n e_j) - f(x-y)}{h_n} dy.
\end{equation}
The integrand converges pointwise to $K \ni y \mapsto \Phi(y) \partial_j f(x-y)$ as $n \to \infty$.
The absolute value of the integrand has the integrable majorant $K \ni y \mapsto |\Phi(y)| \sup\_{ z \in K} \\|f^\prime (z)\\|$. This is a majorant by (a corollary to) the mean value theorem.
Therefore Lebesgues theorem of dominated convergence implies that $u$ is partially differentiable in the $j$-th variable at $x$ and that
\begin{equation}
    \partial\_j u (x)  = \int_K \Phi (y) \partial_j f (x-y) dy = \int\_{\mathbb{R}^m} \Phi(x-y) \partial_j f(y) dy.
\end{equation}
By proposition 1 $\partial\_j u$ is continuous. $\square$
