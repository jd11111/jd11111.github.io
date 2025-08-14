---
layout: post
title:  "Proving the Divergence Theorem and Green's Identities from Stokes Theorem"
date:   2025-08-13 10:00:00 +0200
categories:
---
**Divergence Theorem:**
Let $n \in \mathbb{N}$ and $\Omega \subset \mathbb{R}^n$ a bounded domain with smooth boundary.
Let $N$ be the outwardpointing normal vector field.
Let $U$ be an open neighborhood of $\bar \Omega$ and
$X:= \sum_{j=1}^n F_j \frac{\partial}{\partial x_j}$
be a $C^1$ vector field on $U$.
Then
\begin{equation}
    \int_\Omega \sum_{j=1}^n \partial_j F_j d V = \int_{\partial \Omega} \langle N, X\rangle dS.
\end{equation}
**Proof:**
Let $§$ denote contraction in the first slot.
Let $\omega := X § dV$. Then
\begin{equation}
\omega = \sum\_{j=1}^n (-1)^{j-1} F_j  dx\_1 \wedge \cdots \wedge \widehat{dx}\_j \wedge \cdots  \wedge dx_n.
\end{equation}
From here it follows by applying the definition of $d$ that
\begin{equation}
d \omega = \sum\_{j=1}^n \partial\_j F_j d V .
\end{equation}
Therefore by Stokes theorem
\begin{equation}
\int\_\Omega    \sum\_{j=1}^n \partial\_j F_j d V 
= \int\_\Omega  d \omega
= \int\_{\partial \Omega} \iota^* \omega,
\end{equation}
where $\iota : \partial \Omega \to \bar \Omega$ is the embedding.
By definition $dS = N §\iota^* dV$.
Now let
\begin{equation}
    X^\perp := \langle N, X\rangle N 
\end{equation}
and $Y := X - X^\perp$.
Then by linearity
\begin{equation}
    \iota^* \omega = \iota^* (X § dV) = \iota^* (X^\perp  §d V) + \iota^* (Y § dV)
\end{equation}
and
\begin{equation}
    \iota^* (X^\perp § dV) = \langle N, X\rangle  N § \iota^* dV = \langle N, X \rangle dS.
\end{equation}
Let $v_1, \dots, v_{n-1}$ be any tangent vectors of $\partial \Omega$.
Then
\begin{equation}
     \iota^* (Y § dV) (v_1, \dots, v_{n-1}) = 
dV ( Y, v_1, \dots, v_{n-1}) =0,
\end{equation}
because $Y$ is tangent to $\partial \Omega$ (since $\langle Y, N\rangle =0$) and $n$ vectors from a $n-1$ dimensional vector space must be linearly dependent (as well as $dV$ being a top form).
In total this shows that
\begin{equation}
\int\_\Omega    \sum\_{j=1}^n \partial\_j F_j d V 
= \int\_\Omega  d \omega
= \int\_{\partial \Omega} \iota^* \omega
= \int\_{\partial \Omega} \langle N, X \rangle dS,
\end{equation}
which is the divergence theorem. $\square$

**Green's First Identity:**
In the situation of the divergence theorem:
Let $\varphi, \psi  \in C^2(U)$. Then
\begin{equation}
    \int_{\Omega} \varphi \Delta \psi + \sum_{j=1}^n \partial_j \psi \partial_j  \varphi dV = \int_{\partial \Omega} \varphi \bigg\langle \sum_{j=1}^n \partial_j \psi \frac{\partial }{\partial x_j}, N \bigg\rangle dS.
\end{equation}
**Proof:**
Take $X:= \sum_{j=1}^n \varphi \partial_j \psi \frac{\partial }{\partial x_j}$ in the divergence theorem and use the product rule. $\square$

**Green's Second Identity:**
In the situation of the divergence theorem:
Let $\varphi, \psi  \in C^2(U)$. Then
\begin{equation}
    \int_{\Omega} \varphi \Delta \psi - \Delta \varphi \psi  dV = \int_{\partial \Omega}  \bigg\langle \sum_{j=1}^n \varphi  \partial_j \psi \frac{\partial }{\partial x_j} - \psi  \partial_j \varphi \frac{\partial }{\partial x_j}  , N \bigg\rangle dS.
\end{equation}
**Proof:**
This follows immediatily from Greens first identity (twice) and by noticing that the symmetric terms cancel.$\square$

