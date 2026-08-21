---
layout: post
title:  "Asymptotics of the quotient of two integrals"
date:   2026-08-19 10:00:00 +0200
categories:
---
For $n \in \mathbb{N}$ let $f_n : (0, \infty) \to (0, \infty)$,
\begin{equation\*}
f_n( s) := (4y (1-y))^{2 n}, \quad y := \exp ( -\log (2) t)
\end{equation\*}
and
\begin{equation\*}
c_{1,n} := \int_0^\infty s^{-1} f_n (s) d s, \quad c_{2,n} := \int_0^\infty (s-1)^2 s^{-1} f_n (s) d s.
\end{equation\*}
**Proposition 1:** We have
\begin{equation\*}
\lim_{n \to \infty} (2 n)^{\frac{3}{2}} c_{2,n} = \frac{\sqrt{\pi}}{ 2\log(2)^3}.
\end{equation\*}
**Proof:**
The idea for the proof is to apply Lebesgue's theorem of dominated convergence to conclude that
\begin{equation\*}
\lim_{n \to \infty} (2 n)^{\frac{3}{2}} c_{2,n} = \int_{-\infty}^\infty t^2 \exp ( - \log(2)^2 t^2) dt = \frac{\sqrt{\pi}}{ 2\log(2)^3}.
\end{equation\*}
Let $n \in \mathbb{N}$.
Substituting with $s \mapsto  \sqrt{2 n} (s-1)$ shows that
\begin{equation}
\label{intAfterSub}
c_{2,n}  = \frac{1}{(2n)^{\frac{3}{2}}} \int_{- \sqrt{2n}}^\infty \frac{t^2}{1+\frac{t}{\sqrt{2n}}} f_n \bigg(1+\frac{t}{\sqrt{2n}}\bigg) dt.
\end{equation}
For all $y \in \mathbb{R}$ we have
\begin{equation\*}
4y (1-y) = -4 \bigg(y-\frac{1}{2}\bigg)^2 +1.
\end{equation\*}
And so for all $t  \in (- \sqrt{2n}, \infty)$ it is true that
\begin{equation\*}
 \log \bigg(f_n \bigg(1+\frac{t}{\sqrt{2n}}\bigg) \bigg) =  2n  \log \big( 1-  h_n(t) \big),
\end{equation\*}
where
\begin{equation\*}
h_n (t) := \bigg(\exp \bigg( - \log (2) \frac{t}{\sqrt{2n}}\bigg)-1\bigg)^2.
\end{equation\*}
From the Taylor expansion of the logarithm and the Lagrange form of the remainder it follows that there is $M_1 \in (0, \infty)$ such that for all $x \in [-1/2,1/2]$ it holds that
\begin{equation}
\label{logEstimate}
|\underbrace{\log (1+x) - x}\_{ =:R_1(x)} |\leq M_1 x^2.
\end{equation}
Similarly it follows that there is $M_2 \in (0,\infty)$ such that for all $x \in  [-1,1]$ we have
\begin{equation}
\label{expEstimate}
 |\underbrace{(\exp (x) - 1)^2 - x^2}\_{ =:R_2(x)} |\leq M_2 |x|^3.
\end{equation}
Let $t \in \mathbb{R}$ and $n \in \mathbb{N}$ such that $- \sqrt{2n} <t$. Then
\begin{equation\*}
2n  \log \big( 1- h_n(t) \big) = 2n (- h_n(t) + R_1(-h_n(t)))
\end{equation\*}
and
\begin{equation\*}
 \- 2n h_n(t)  = - 2n \log (2)^2 \frac{t^2}{2n}  - 2n R_2\bigg( - \log (2) \frac{t}{\sqrt{2n}}\bigg).
\end{equation\*}
Now combining \eqref{logEstimate} and \eqref{expEstimate} shows that
\begin{equation\*}
\lim_{n \to \infty}R_1(-h_n(t))) =0, \ \lim_{n \to \infty}2n R_2\bigg( - \log (2) \frac{t}{\sqrt{2n}}\bigg)=0.
\end{equation\*}
Therefore
\begin{equation\*}
\lim_{n \to \infty} 2n  \log \big( 1- h_n(t) \big)  =  - \log(2)^2 t^2.
\end{equation\*}
This shows that the integrand in \eqref{intAfterSub} converges pointwise to $t \mapsto t^2 \exp ( - \log(2)^2t^2)$ for $n \to \infty$.

To apply Lebesgue's theorem of dominated convergence it is left to find a majorant for the integrand. Recall that for all $x \in \mathbb{R}$ we have
\begin{equation\*}
1+x \leq e^x.
\end{equation\*}
This implies, for all $x \in \mathbb{R}$, that
\begin{equation}
\label{logIneq}
\log( 1+x ) \leq x
\end{equation}
and
\begin{equation}
\label{ExpSqIneq}
 -(e^x-1)^2 \leq -x^2.
\end{equation}
Let $n \in \mathbb{N}$ and $t \in ( - \sqrt{2n}, \infty)$. Then using the inequalities \eqref{logIneq} and \eqref{ExpSqIneq} shows that
\begin{equation\*}
2n  \log \big( 1- h_n(t) \big) \leq - 2n h_n(t) \leq -2n \log(2)^2 \frac{t^2}{2n}.
\end{equation\*}
This shows that the integrand in \eqref{intAfterSub} is majorized by $t \mapsto t^2 \exp ( - \log(2)^2 t^2)$. $\square$

**Proposition 2:**
We have
\begin{equation\*}
\lim_{n \to \infty} \sqrt{2 n} c_{2,n} = \frac{\sqrt{\pi}}{ \log(2)}.
\end{equation\*}
**Proof:**
The idea for the proof is to apply Lebesgue's theorem of dominated convergence to conclude that
\begin{equation\*}
\lim_{n \to \infty} \sqrt{2 n} c_{2,n} = \int_{-\infty}^\infty \exp ( - \log(2)^2 t^2) dt = \frac{\sqrt{\pi}}{\log(2)}.
\end{equation\*}
The remainder of the proof is pretty much the same as the proof of Proposition 1. $\square$

**Corollary:**
We have
\begin{equation\*}
\lim_{n \to \infty} 4 n \log(2)^2 \frac{c_{2,n}}{c_{1,n}} =  1.
\end{equation\*}
**Proof:**
For all $n \in \mathbb{N}$ it holds that
\begin{equation\*}
 2n\frac{c_{2,n}}{c_{1,n}} = \frac{(2n)^{\frac{3}{2}}c_{2,n}}{ \sqrt{2n} c_{1,n}}.
\end{equation\*}
Therefore Proposition 1 and 2 and the rules for the calculation of limits show that
\begin{equation\*}
\lim_{n \to \infty} 2n\frac{c_{2,n}}{c_{1,n}} = \frac{1}{2 \log(2)^2}. \ \square
\end{equation\*}

