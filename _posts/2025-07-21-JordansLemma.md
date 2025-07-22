---
layout: post
title:  "Jordans Lemma"
date:   2025-07-20 10:00:00 +0200
categories:
---
In this post i will prove:

**Jordans Lemma:**
Let $\alpha \in (0, \infty)$, $R \in (0, \infty)$, $\gamma_R : [0, \pi] \to \mathbb{C}$, $\gamma_R(t):= R \exp (it)$ and $f: \gamma\_R ([0, \\pi]) \to \mathbb{C}$ continuous.
Then
\begin{equation}
\bigg| \int_{\gamma_R} \exp ( \alpha i z) f (z) dz \bigg| \leq 
M_R \frac{\pi}{\alpha},
\end{equation}
where $M_R:= \max_{ t \in [0, \pi]} |f(R e^{it})|$.

**Proof:**
By definition of the curve integral:
\begin{equation}
\bigg| \int_{\gamma_R} \exp ( \alpha i z) f (z) dz \bigg|
=\bigg| \int_0^{\pi} \exp ( \alpha i R e^{it}) f (r e^{it}) r e^{it} dt \bigg|.
\end{equation}
Moving the absolute value into the integral:
\begin{equation}
\bigg| \int_0^{\pi} \exp ( \alpha i R e^{it}) f (R e^{it}) R e^{it} dt \bigg|
\leq \int_0^{\pi} |\exp ( \alpha i R e^{it})| |f (R e^{it})| R |e^{it}| dt
\end{equation}
and therefore using the monotonicity of the integral:
\begin{equation}
 \bigg| \int_{\gamma_R} \exp ( \alpha i z) f (z) dz \bigg|
\leq M_R R  \int_0^{\pi} |\exp ( \alpha i R e^{it})| dt.
\end{equation}
It is left to estimate the integral.
In general: $\forall z := x+iy \in \mathbb{C}: |e^z | = e^{x}$ and therefore for all $t \in [0,\pi]$:
\begin{equation}
    |\exp ( \alpha i R e^{it})| = \exp (- \alpha R \sin (t) )
\end{equation}
where $e^{it} = \cos (t) + i \sin (t)$ was used.
Therefore
\begin{equation}
    \int_0^{\pi} |\exp ( \alpha i R e^{it})| dt = \int_0^\pi \exp (- \alpha R \sin (t) )dt
\end{equation}
The idea now is to show that
\begin{equation}
\int_0^\pi \exp (- \alpha R \sin (t) )dt = 2\int_0^\pi \exp (- \alpha R \sin (t) )dt 
\end{equation}
and to then use that $\sin$ is concave on $[0,\pi/2]$ together with the monotonicity of the exponential function to estimate the integral from above.
Define $\varphi : [0,\pi] \to [0,\pi]$, $\varphi (t):= (\pi -t)$.
Then $\varphi^\prime =-1$ and $\forall t \in [0,\pi]$: $\sin (\varphi (t) ) = \sin(t)$ (follows from addition theorem).
Using substitution:
\begin{equation}
 \int_0^{\pi/2} \varphi^\prime (t) \exp (- \alpha R \sin (\varphi (t)) )dt
= \int_{\varphi (0)}^{\varphi(\pi)}\exp (- \alpha R \sin (t) )dt
\end{equation}
and so
\begin{equation}
 \-    \int_0^{\pi/2} \exp (- \alpha R \sin (t))dt
=  \int_\pi^{\pi/2} \exp (- \alpha R \sin (t) )dt
\end{equation}
From here it follows from the basic integration rules that
\begin{equation}
     \int_0^{\pi} \exp (- \alpha R \sin (t))dt
= 2 \int_0^{\pi/2} \exp (- \alpha R \sin (t))dt.
\end{equation}
Now $\sin$ is concave on $[0,\pi/2]$ (follows from the derivative characterisation).
Therefore by definition of concavity $\forall x_1, x_2 \in \mathbb [0,\pi/2]$ and $\lambda \in [0,1]$:
\begin{equation}
    \sin (x_1 \lambda + x_2 (1-\lambda)) \geq \lambda \sin (x_1) + (1-\lambda) \sin (x_2). 
\end{equation}
Let $y \in [0, \pi/2]$.
Choosing $x_2 =0$, $x_1 = \pi/2$ and $\lambda = y /(\pi /2)$ in the above:
\begin{equation}
    \sin ( y) \geq \frac{y}{\pi /2} \Rightarrow - \sin ( y) \leq -\frac{y}{\pi /2}.
\end{equation}
Since $\exp$ (on $\mathbb{R}$) and the integral are monotone:
\begin{equation}
\int_0^{\pi/2} \exp (- \alpha R \sin (t))dt \leq 
\int_0^{\pi/2} \exp (- \alpha R \frac{t}{\pi /2} )dt 
\end{equation}
and
\begin{equation}
\int_0^{\pi/2} \exp (- \alpha R \frac{t}{\pi /2} )dt 
= \frac{-\pi}{2\alpha R} ( \exp (- \alpha R) - 1) \leq \frac{\pi}{2\alpha R},
\end{equation}
since $\exp \geq 0$ on $\mathbb{R}$.
Putting everything together:
\begin{equation}
 \bigg| \int_{\gamma_R} \exp ( \alpha i z) f (z) dz \bigg|
\leq M_R R  \int_0^{\pi} |\exp ( \alpha i R e^{it})| dt
\leq  M_R R 2 \frac{\pi}{2\alpha R} = M_R \frac{\pi}{\alpha}.
\end{equation}
Which ends the proof. $\square$


