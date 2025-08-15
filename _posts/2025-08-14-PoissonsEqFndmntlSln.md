---
layout: post
title:  "Solving Poisson's Equation with the Fundamental Solution"
date:   2025-08-13 10:00:00 +0200
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

**Proposition 1 ($\Phi$ is the fundamental solution of $-\Delta$):**
Let $f \in C_c^2(\mathbb{R}^n)$.
Then
\begin{equation}
    \int_{\mathbb{R}^n}  -\Delta f \Phi dV = f(0).
\end{equation}
**Proof:**
Let $R \in (0, \infty)$ such that the support of $f$ is contained in $B(0,R)$.
Then
\begin{equation}
     \int_{\mathbb{R}^n}  \Delta f \Phi dV  = \lim_{\varepsilon \to 0} \int_{B(0,R) \setminus \bar B (0, \varepsilon)}  \Delta f \Phi dV .
\end{equation}
Let $\varepsilon \in (0, R)$ and $\Omega_\varepsilon := B(0,R) \setminus \bar B (0, \varepsilon)$.
By Green's second identity:
\begin{equation}
    \int_{\Omega_\varepsilon}  \Delta f \Phi dV 
=    \int_{\Omega_\varepsilon} f \Delta \Phi dV  + \int_{\partial \Omega_\varepsilon} \Phi (x)  \langle  \nabla f (x) , N (x) \rangle  dS(x) -
\int_{\partial \Omega_\varepsilon} f (x)  \langle  \nabla \Phi (x) , N (x) \rangle  dS(x) ,
\end{equation}
where $N$ is the outer surface normal vectorfield and $dS$ the surface measure of $\partial \Omega_\varepsilon$.
Since $f$ vanishes on $\partial B(0,R)$ and using the Cauchy-Schwarz inequality it follows that
\begin{equation}
\bigg|\int_{\partial \Omega_\varepsilon} \Phi (x)  \langle  \nabla f (x) , N (x) \rangle  dS(x)\bigg|
\leq \sup_{x \in \mathbb{R}^n} \\| \nabla f (x)\\| \int_{\partial B(0, \varepsilon)} \Phi dS
\end{equation}
and
\begin{equation}
\int_{\partial B(0, \varepsilon)} \Phi dS = \frac{1}{(n-2) n\alpha(n)} \frac{1}{ \varepsilon^{n-2}} n \alpha(n)  \varepsilon^{n-1} = \frac{1}{n-2} \varepsilon.
\end{equation}
Now since $f$ vanishes on $\partial B(0,R)$, by the formula for the partial derivatives of $\Phi$ and the formula for the surface normal vector field:
\begin{equation}
\-\int_{\partial \Omega_\varepsilon} f (x)  \langle  \nabla \Phi (x) , N (x) \rangle  dS(x)
= -\frac{1}{n \alpha(n) \varepsilon^{n-1}}  \int_{\partial B(0,\varepsilon)} f (x) dS(x).
\end{equation}
Putting equation (6), (8), (9) and (5) together:
\begin{equation}
 \int_{\mathbb{R}^n}  \Delta f \Phi dV 
= \lim_{\varepsilon \to 0 }  -\frac{1}{n \alpha(n) \varepsilon^{n-1}}  \int_{\partial B(0,\varepsilon)} f (x) dS(x) = - f(0),
\end{equation}
because $f$ is continuous. $\square$

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
    - \Delta u (x) = \int\_{\mathbb{R}^n}  -\Delta f(x-y) \Phi (y) d V(y) =  f(x),
\end{equation}
where the last equality is due to proposition 1 applied to $f(x-\bullet)$. $\square$
