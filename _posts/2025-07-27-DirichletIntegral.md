---
layout: post
title:  "Calculating the Dirichlet Integral using Complex Analysis"
date:   2025-07-27 10:00:00 +0200
categories:
---
In this post i will prove, that the **Dirichlet Integral** is equal to $\pi/2$ (see corollary below) by using complex analysis techniques.
The following integral is more amenable to complex analysis techniques:

**Proposition:**
\begin{equation}
    \lim_{R \to \infty} \int_{-R}^R \frac{\sin (x)}{x} dx  = \pi
\end{equation}
**Proof:**
Note: The integrand can be continuously extended to $0$ by $1$, because $\lim_{x \to 0} \sin (x) /x =1$.
Let $R \in [1,\infty)$. Then 
\begin{equation}
\int_{-R}^R \frac{\sin (x)}{x} dx  = \lim_{(0,1) \ni \varepsilon \to 0} \bigg( \int_{-R}^{-\varepsilon} \frac{\sin (x)}{x} dx + 
 \int_{\varepsilon}^{R} \frac{\sin (x)}{x} dx \bigg)
\end{equation}
Let $\varepsilon \in (0,1)$.
Then (using $\forall z \in \mathbb{C}: \exp ( iz) = \cos(z) + i \sin (z)$)
\begin{equation}
     \int_{-R}^{-\varepsilon} \frac{\sin (x)}{x} dx + 
 \int_{\varepsilon}^{R} \frac{\sin (x)}{x} dx 
= \Im \bigg (  \int_{[-R,-\varepsilon]} \frac{e^{iz}}{z} dz + 
 \int_{[\varepsilon,R]} \frac{e^{iz}}{z} dz 
\bigg).
\end{equation}
For $\varepsilon \in (0,1)$ let $\gamma_\varepsilon: [0, \pi]\to \mathbb{C}$, $\gamma_\varepsilon (t) := -\varepsilon e^{-it}$.
For $R \in [1,\infty)$ let
$\beta_R :[0,\pi] \to \mathbb{C}$, $\beta_R (t):= R e^{it}$.
By Cauchys integral theorem: $\forall R \in [1,\infty), \varepsilon \in (0,1)$:
\begin{equation}
    \int_{[\varepsilon,R]\beta_R [-R,-\varepsilon] \gamma_\varepsilon} \frac{e^{iz}}{z}dz=0.
\end{equation}
Therefore
\begin{equation}
  \int_{[-R,-\varepsilon]} \frac{e^{iz}}{z} dz + 
\int_{[\varepsilon,R]} \frac{e^{iz}}{z} dz 
= -\int_{\gamma_\varepsilon} \frac{e^{iz}}{z} dz - \int_{\beta_R}  \frac{e^{iz}}{z} dz .
\end{equation}
By using the power series of the exponential function it follows that $\mathbb{C}\setminus \\{0\\} \ni z \mapsto \frac{e^{iz}}{z} - \frac{1}{z}$ can be holomorphically extended to $\mathbb{C}$.
By the fundamental estimate
\begin{equation}
\bigg|\int_{\gamma_\varepsilon} \frac{e^{iz}}{z} - \frac{1}{z}dz\bigg| 
\leq \pi \varepsilon \max_{z \in \bar D_1(0)} \bigg|\frac{e^{iz}}{z}- \frac{1}{z}\bigg|  \to 0 \quad  (\varepsilon \to 0).
\end{equation}
Now
\begin{equation}
    \int_{\gamma_\varepsilon} \frac{1}{z} dz = 
\int_0^\pi \frac{1}{-\varepsilon e^{-it} } i \varepsilon e^{-it} dt = -i \pi.
\end{equation}
By combining Eq. (6) and (7):
\begin{equation}
 \lim_{(0,1) \ni \varepsilon \to 0}   \int_{\gamma_\varepsilon} \frac{e^{iz}}{z} dz = -i \pi.
\end{equation}
Using Jordan's lemma (see my previous blog post):
\begin{equation}
\bigg|\int_{\beta_R}  \frac{e^{iz}}{z} dz \bigg|
\leq \frac{\pi}{R} \to 0  \quad  ( R\to \infty).
\end{equation}
And so in total, combining Eq. (5), (8) and (9):
\begin{equation}
 \lim_{R \to \infty} \lim_{(0,1) \ni\varepsilon \to 0} \bigg( \int_{[-R,-\varepsilon]} \frac{e^{iz}}{z} dz + 
\int_{[\varepsilon,R]} \frac{e^{iz}}{z} dz \bigg)
= i \pi.
\end{equation}
Since $\Im$ is continuous we obtain from Eq. (3) and (2)
\begin{equation}
 \lim_{R \to \infty}   \int_{-R}^R \frac{\sin(x)}{x}dx = 
\pi.
\end{equation}
This ends the proof. $\square$

**Corollary (Dirichlet Integral):**
\begin{equation}
    \lim_{R \to \infty} \int_0^R  \frac{\sin (x)}{x} dx  = \frac{\pi}{2}.
\end{equation}
**Proof:**
This follows from the proposition, because for all $x \in \mathbb{R} \setminus \\{0\\}$:
\begin{equation}
    \frac{\sin (x)}{x} = \frac{\sin (-x)}{-x},
\end{equation}
since $\sin$ is an odd function.
Now define $\varphi :\mathbb{R}\to \mathbb{R}$, $\varphi (x) := -x$.
Then $\varphi^\prime =-1$.
Let $R \in [0,\infty)$:
By the substitution rule
\begin{equation}
    \int_{-R}^0 \frac{\sin (x)}{x}dx = -\int_{-R}^0 \varphi^\prime (y) \frac{\sin (\varphi(y))}{\varphi(y)}dy
=-\int_{\varphi(-R)}^{\varphi (0)} \frac{\sin (x)}{x}dx 
= \int_0^R  \frac{\sin (x)}{x}dx .
\end{equation}
Therefore
\begin{equation}
    \int_{-R}^R \frac{\sin (x)}{x}dx 
=    \int_{-R}^0 \frac{\sin (x)}{x}dx +\int_{0}^R \frac{\sin (x)}{x}dx 
= 2 \int_{0}^R \frac{\sin (x)}{x}dx 
\end{equation}
and so the proposition implies the corollary. $\square$

