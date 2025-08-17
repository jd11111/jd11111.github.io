---
layout: post
title:  "Solving Poisson's Equation with the Fundamental Solution"
date:   2025-08-14 10:00:00 +0200
categories:
---
Let $n \in \mathbb{R}^n$ with $n\geq 3$.
Let $\alpha (n)$ be the volume of the unit ball $B(0,1)$.
Then the surface area of $\partial B(0,1)$ is $n \alpha(n)$.
Define the **fundamental solution** $\Phi: \mathbb{R}^n \setminus \\{0\\}\to \mathbb{R}$ of $-\Delta$ by
\begin{equation}
    \Phi(x):= \frac{1}{(n-2) n\alpha(n)} \frac{1}{\\| x \\|^{n-2}}.
\end{equation}
The fundamental solution has the following easily verified (for 5. integrate in a ball centered at $0$ and use spherical coordinates) properties:
1. $\Phi \in C^\infty (\mathbb{R}^n \setminus \\{0\\})$,
2. $\forall j \in \\{1,\dots,n \\}, x \in \mathbb{R}^n\setminus \\{0\\}$:
\begin{equation}
    \partial_j \Phi (x) =  - \frac{1}{n \alpha (n)} \frac{x_j}{\\| x\\|^n},
\end{equation}
3. $\forall j ,k \in \\{1,\dots,n \\}, x \in \mathbb{R}^n\setminus \\{0\\}$:
\begin{equation}
    \partial_k \partial_j \Phi (x) =  - \frac{1}{n \alpha (n)} \bigg( \frac{\delta_{j,k}}{\\| x\\|^n} -n \frac{x_k x_j}{ \\| x \\|^{n+2}} \bigg),
\end{equation}
4. $- \Delta \Phi =0$,
5. $\Phi \in L^1_{\mathrm{loc}} (\mathbb{R}^n)$.

**Proposition 1 (Green's representation formula):**
Let $\Omega \subset \mathbb{R}^n$ be a bounded domain with $C^2$-boundary.
Let $V \subset \mathbb{R}^n$ open with $\bar \Omega \subset V$ and $u \in C^2(V)$.
Then for all $x \in \Omega$:
\begin{equation}
    u(x) = -\int\_{\Omega}  \Delta u \Psi dV +
 \int\_{\partial \Omega} \Psi \langle  \nabla u , N \rangle - u  \langle  \nabla \Psi , N \rangle   dS ,
\end{equation}
where $\Psi := \Phi (\bullet-x)$.

**Proof:**
Let $\varepsilon \in (0, \infty)$ so that $\bar B(x,\varepsilon) \subset \Omega$.
Let $\Omega_\varepsilon := \Omega \setminus \bar B (x, \varepsilon)$.
By the chain rule for all $j  \in \\{1,\dots, n\\}$ and $y \in \mathbb{R}^n \setminus \\{ x\\}$: $\partial_j \Psi ( y) = \partial_j \Phi (y-x)$ and $\Delta \Psi = \Delta \Phi =0$.
By Green's second identity:
\begin{equation}
\begin{split}
     \int\_{\Omega_\varepsilon}  \Delta u \Psi dV &=    \underbrace{\int_{\Omega_\varepsilon} u \Delta \Psi dV}\_{=0}  + \int_{\partial \Omega_\varepsilon} \Psi \langle  \nabla u , N \rangle   - u  \langle  \nabla \Psi , N \rangle  dS,\\\\ 
&=\int\_{\partial \Omega} \Psi \langle  \nabla u , N \rangle   - u  \langle  \nabla \Psi , N \rangle  dS  + \int_{\partial B(x, \varepsilon)} \Psi \langle  \nabla u , N \rangle   - u  \langle  \nabla \Psi , N \rangle  dS,
\end{split}
\end{equation}
where $N$ is the outer surface normal vectorfield and $dS$ the surface measure of $\partial \Omega_\varepsilon$.
Now, using the Cauchy-Schwarz inequality and spherical coordinates:
\begin{equation}
 \bigg|\int_{\partial B(x, \varepsilon)} \Psi \langle  \nabla u , N \rangle dS  \bigg|
\leq \sup_{y \in \Omega} \\| \nabla u \\|
\int_{\partial B(0, \varepsilon)} \Phi dS
\end{equation}
and
\begin{equation}
\int_{\partial B(0, \varepsilon)} \Phi dS = \frac{1}{(n-2) n\alpha(n)} \frac{1}{ \varepsilon^{n-2}} n \alpha(n)  \varepsilon^{n-1} = \frac{1}{n-2} \varepsilon.
\end{equation}
By definition of $N$ (pointing inwards!) and the formula for $\nabla \Phi$:
\begin{equation}
 \int_{\partial B(x, \varepsilon)} - u  \langle  \nabla \Psi , N \rangle  dS
= - \frac{1}{n \alpha (n) \varepsilon^{n-1}} \int_{\partial B(x, \varepsilon)} u   dS \to -u (x) \ (\varepsilon  \to  0).
\end{equation}
The limit follows from the fact that $u$ is continuous and that $n \alpha (n) \varepsilon^{n-1}$ is the surface area of $\partial B(x,\varepsilon)$.
Therefore by combining the preceding
\begin{equation}
    \int\_{\Omega}  \Delta u \Psi dV 
= \lim_{\varepsilon \to 0} \int_{\Omega_\varepsilon}
 \Delta u \Psi dV 
= \int\_{\partial \Omega} \Psi \langle  \nabla u , N \rangle   - u  \langle  \nabla \Psi , N \rangle  dS - u(x). \quad \square
\end{equation}

**Remark:**
In the situation of the preceding: If $\Delta u=0$ then Green's representation formula shows that the values of $u$ in $\Omega$ are determined only by the values of $u$ on $\partial \Omega$.
This is similar to Cauchys integral formula in complex analysis.

**Proposition 1 ($\Phi$ is the fundamental solution of $-\Delta$):**
Let $f \in C_c^2(\mathbb{R}^n)$ and $x \in \mathbb{R}^n$.
Then
\begin{equation}
    \int_{\mathbb{R}^n}  -\Delta f(y) \Phi(y-x) dV(y) = f(x).
\end{equation}
**Proof:**
Let $R \in (0, \infty)$ such that the support of $f$ is contained in $B(0,R)$.
Then according to Green's representation formula
\begin{equation}
     \int_{\mathbb{R}^n}  -\Delta f(y) \Phi(y-x) dV(y)  =     \int_{B(0,R)}  -\Delta f(y) \Phi(y-x) dV(y)  =f (x). \ \square
\end{equation}

**Proposition 2 (solving Poisson's equation in $\mathbb{R}^n$):**
Let $f \in C^2_c (\mathbb{R}^n)$. Let $u : \mathbb{R}^n \to \mathbb{R}$,
\begin{equation}
u(x):= \int\_{\mathbb{R}^n} \Phi(y) f(x-y)d V(y).
\end{equation}
Then $u \in C^2(\mathbb{R}^n)$ and $- \Delta u =f$.

**Proof:**
Since $\Phi$ is locally integrable $u$ is well defined.
By the theorem of differentiation under the integral sign $u\in C^2(\mathbb{R}^n)$ and for all $x \in \mathbb{R}^n$:
\begin{equation}
    - \Delta u (x) = \int\_{\mathbb{R}^n}  -\Delta f(x-y) \Phi (y) d V(y) 
=  \int\_{\mathbb{R}^n}  -\Delta f(y) \underbrace{\Phi (x-y)}\_{= \Phi (y-x)} d V(y)  = f(x),
\end{equation}
by the preceding proposition. $\square$
