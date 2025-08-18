---
layout: post
title:  "The Method of the Green's Function for the Laplacian"
date:   2025-08-17 10:00:00 +0200
categories:
---
Let $n \in \mathbb{N}$ and
Let $\Omega \subset \mathbb{R}^n$ a bounded region with smooth boundary.
Let $\Phi$ be the fundamental solution of $-\Delta$ (see previous post on the topic).
Suppose that for all $x \in \Omega$ there exists (a necessarily unique by a corollary to the maximum principle)
$\varphi \in C^2 (\bar \Omega)$ with
\begin{equation}
    \begin{cases}
        \Delta \varphi = 0 , \ \text{on} \ \Omega, \\\\ 
\varphi = \Phi (\bullet-x) , \ \text{on} \ \partial \Omega.
    \end{cases}
\end{equation}

**Definition:**
The **Green's function** $G: \Omega \times \bar \Omega \setminus \\{ (x,y) \in \Omega \times \bar \Omega : x =y \\} \to \mathbb{R}$ of $\Omega$ is defined
by 
\begin{equation}
    G(x,y) := 
         \Phi (x-y) - \varphi(y) ,
\end{equation}
where $\varphi$ is the unique function $\varphi \in C^2 (\bar \Omega)$ with
\begin{equation}
    \begin{cases}
        \Delta \varphi = 0 , \ \text{on} \ \Omega, \\\\ 
\varphi = \Phi (\bullet-x) , \ \text{on} \ \partial \Omega.
    \end{cases}
\end{equation}

**Proposition 1 (representation formula with the Green's function):**
Let $u \in C^2(\bar \Omega)$. Then for all $ x\in \Omega$
\begin{equation}
    u(x) = \int_\Omega -\Delta u G(x,\bullet) dV - \int_{\partial \Omega} u \langle \nabla G(x,\bullet ) , N \rangle dS.
\end{equation}

**Proof:**
Let $x \in \Omega$.
Let 
 $\varphi$ be the unique function $\varphi \in C^2 (\bar \Omega)$ with
\begin{equation}
    \begin{cases}
        \Delta \varphi = 0 , \ \text{on} \ \Omega, \\\\ 
\varphi = \Phi (\bullet-x) , \ \text{on} \ \partial \Omega.
    \end{cases}
\end{equation}
By Green's representation formula (see my post on the fundamental solution) with $N$ the outer surface normal vector:
\begin{equation}
    u(x) = -\int\_{\Omega}  \Delta u \Phi (\bullet-x) dV +
 \int\_{\partial \Omega} \Phi(\bullet -x) \langle  \nabla u , N \rangle - u  \langle  \nabla \Phi(\bullet -x) , N \rangle   dS .
\end{equation}
Applying Green's second formula:
\begin{equation}
    \int_\Omega \phi  \Delta u dV = \underbrace{\int_\Omega \Delta \phi u dV}\_{=0}  + \int_{\partial \Omega}  \phi \langle \nabla u, N \rangle  - u \langle \nabla \phi , N \rangle dS
\end{equation}
Since $\phi = \Phi (\bullet-x)$ on $\partial \Omega$:
\begin{equation}
    u(x) = -\int\_{\Omega}  \Delta u (\Phi (\bullet-x)- \phi) dV -
 \int\_{\partial \Omega}   u  \langle  \nabla (\Phi(\bullet -x)- \phi)  , N \rangle   dS .
\end{equation}
Which is the desired conclusion. $\square$

**Remark:**
The representation formula shows if $f \in C(\Omega)$, $g \in C(\partial \Omega)$ and $u \in C^2(\bar \Omega)$ with $-\Delta u = f$ on $\Omega$ and $u = g$ on $ \partial \Omega$. Then $u$ is completly determined by $f$ and $g$.
It also gives the perfect candidate for a solution.

**Proposition 2:**
Assume $n>2$.
Then $\varphi : \bar B(0,1) \to \mathbb{R}$
\begin{equation}
    \varphi (y) :=  \frac{1}{n (n-2) \alpha(n)},
\end{equation}
where $\alpha(n)$ is the volume of $B(0,1)$,
satisfies $\varphi \in C^2 (\bar \Omega)$ and
\begin{equation}
    \begin{cases}
        \Delta \varphi = 0 , \ \text{on} \ B(0,1), \\\\ 
\varphi = \Phi  , \ \text{on} \ \partial B(0,1).
    \end{cases}
\end{equation}
Let $x \in B(0,1) \setminus \\{0\\}$.
Let $\tilde{x} := \frac{x}{\\|x\\|}$.
Then $\varphi : \bar B(0,1) \to \mathbb{R}$
\begin{equation}
    \varphi (y):= \Phi ( \\|x\\| (y-\tilde{x})) 
\end{equation}
satisfies $\varphi \in C^2 (\bar B(0,1))$ and
\begin{equation}
    \begin{cases}
        \Delta \varphi = 0 , \ \text{on} \ B(0,1), \\\\ 
\varphi = \Phi(\bullet -x)  , \ \text{on} \ \partial B(0,1).
    \end{cases}
\end{equation}

**Proof:**
The first part is obvious.
For the second part:
Since $\\|\tilde{x}\\| >1$ it follows that $\varphi$ is well defined and $\varphi \in C^2(\bar B(0,1))$.
Let $y \in \bar B(0,1)$.
Then
\begin{equation}
   \\|x\\|^2 \\| ( y-\tilde{x})\\|^2 = \\|x\\|^2 \\|y\\|^2 - 2 \langle x, y\rangle +1.
\end{equation}
and therefore if $y \in \partial B(0,1)$ then
\begin{equation}
    \\|x\\|^2 \\| ( y-\tilde{x})\\|^2 = \\| x- y\\|^2.
\end{equation}
This shows $\phi = \Phi (\bullet -x)$ on $\partial B(0,1)$.
A simple (but tedious) calculation shows that $\Delta \varphi =0$ on $B(0,1)$. $\square$

**Proposition 3 (Green's function of $B(0,1)$):**
Assume $n>2$.
Let
\begin{equation}
    \begin{split}
&G: B(0,1) \times \bar B(0,1) \setminus \\{ (x,y) \in B(0,1) \times \bar B(0,1) : x =y \\} \to \mathbb{R} \\\\ 
    &G(x,y):= \Phi (x-y) - \frac{1}{n (n-2)\alpha(n)} \big( \\|x\\|^2 \\|y\\|^2 - 2 \langle x,y \rangle +1 \big)^{\frac{2-n}{2}}.
    \end{split}
\end{equation}
Then $G$ is the Green's function of $B(0,1)$ and for all $x\in B(0,1), y \in \partial B(0,1)$:
\begin{equation}
  \langle  \nabla G(x, \bullet) (y), N (y) \rangle = -\frac{1- \\|x\\|^2}{n \alpha (n)} \frac{1}{\\| x-y \\|^n},
\end{equation}
where $N$ is the outer surface normal vector of $B(0,1)$.

**Proof:**
Follows from proposition 2 and an elementary calculation. $\square$

Armed with the Green's function for $B(0,1)$ and the representation formula it is natural to conjecture:

**Proposition 4 (Poisson formula for $B(0,1)$):**
Let $g\in C(\partial B(0,1))$ and define $u : \bar B(0,1) \to \mathbb{R}$ by 
\begin{equation}
    u(x):= \begin{cases}
        g (x) , \quad  \ x \in \partial B(0,1), \\\\ 
\frac{1- \\|x\\|^2}{n \alpha (n)}\int_{\partial B(0,1)}\frac{g(y)}{\\| x-y \\|^n} dS(y), \quad x \in B(0,1).
    \end{cases}
\end{equation}
Then $u \in C(\bar \Omega) \cap C^2 (\Omega)$, $\Delta u =0$ on $\Omega$ and $u=g$ on $\partial B(0,1)$.

**Proof:**
From the representation formula (and equation 16) with the constant $1$ function we get $\forall x \in B(0,1)$:
\begin{equation}
    1 = \frac{1- \\|x\\|^2}{n \alpha (n)}\int_{\partial B(0,1)}\frac{1}{\\| x-y \\|^n} dS(y).
\end{equation}
This allows to differentiate under the integral sign, showing that $u \in C^2(\Omega)$ and a tedious calculation shows that $\Delta u =0$.
It is left to show the continuity of $u$:
Let $x_0 \in \partial B(0,1)$ and $\varepsilon \in (0, \infty)$.
Let $\delta \in (0, \infty)$ such that for all $y \in \partial B(0,1)$:
\begin{equation}
\\|y-x_0\\| <\delta \Rightarrow |g(y)-g(x_0)| < \varepsilon.
\end{equation}
Let $\tilde{\delta} \in (0, \delta /2)$.
Let $x \in B(0,1)$ with $\\|x-x_0\\|< \tilde{\delta}$. Then
\begin{equation}
\begin{split}
   | u(x) - u(x_0) | &\leq \int_{\partial B(0,1)} |g(y)- g(x_0)|  \frac{1- \\|x\\|^2}{n \alpha (n) \\|x-y\\|^n}dS(y) \\\\ 
& \leq  \int_{\partial B(0,1) \cap B(x, \delta/2)} |g(y)- g(x_0)|  \frac{1- \\|x\\|^2}{n \alpha (n) \\|x-y\\|^n}dS(y) \\\\ 
&+ \int_{\partial B(0,1) \setminus  \bar B(x, \delta/2)} |g(y)- g(x_0)|  \frac{1- \\|x\\|^2}{n \alpha (n) \\|x-y\\|^n}dS(y) \\\\ 
&\leq \varepsilon  + (1- \\|x\\|^2) \sup_{ y \in \partial B(0,1)} |g (y)|  (\delta/2)^{-n}.
\end{split}
  \end{equation}
From which the proposition follows by choosing $\tilde{\delta}$ appropriatly small. $\square$


