---
layout: post
title:  "The Mean Value Property for Laplace's Equation and its Consequences"
date:   2025-08-16 10:00:00 +0200
categories:
---
Let $n \in \mathbb{N}$ and $\Omega \subset \mathbb{R}^n$ a bounded domain.
Let $\alpha(n)$ be the volume of $B(0,1)$.

**Proposition 1:**
Let $u \in C^2(\Omega)$ and $x \in \Omega$.
Let $r_0 \in (0, \infty)$ such that $ B(x,r_0 ) \subset \Omega$.
Define $\varphi : [0, r_0) \to \mathbb{R}$ by
\begin{equation}
    \varphi (r):=
\begin{cases}
    u(x), \ \text{if} \ r=0, \\\\ 
\frac{1}{n \alpha(n)r^{n-1}} \int_{\partial B(x,r)} u dS, \ \text{else.}
\end{cases}
\end{equation}
Then $\varphi$ has the following properties:
1. $\varphi$ is continuous.
2. $\varphi$ is differentiable on $(0,r_0)$ and $\forall r \in (0, r_0)$:
\begin{equation}
    \varphi^\prime (r) =  \frac{1}{n \alpha(n) r^{n-1}}  \int_{B(x,r)} \Delta u  dV.
\end{equation}
In particular $\varphi^\prime$ can be extended continuously to $0$ by $0$.
3. (the continuous extension of) $\varphi^\prime$ is differentiable and
\begin{equation}
\varphi^{\prime \prime }(0) = \frac{1}{n} \Delta u (x).
\end{equation}
4. \begin{equation}
    \Delta u (x) = \lim_{(r_0, 0) \ni r \to 0} \frac{2n}{r^2} \bigg (\frac{1}{n \alpha(n) r^{n-1}}\int_{\partial B(x,r) } u(y)dy  -u (x)  \bigg).
\end{equation}

**Proof:**
By continuity of $u$, $\lim_{r \to 0} \varphi (r) = u(x) = \varphi(0)$ and so $\varphi$ is continuous at $0$ (using that $r^{n-1} n \alpha(n)$ is the surface area of $\partial B(x,r)$).
Inserting spherical coordinates shows that $\forall r \in (0, r_0)$:
\begin{equation}
    \varphi (r) = \frac{1}{n \alpha(n)} \int_{\partial B(0,1)} u(x+ry) dS(y).
\end{equation}
By the theorem of differentiation under the integral sign $\varphi$ is twice continously differentiable on $(0,r_0)$ and $\forall r \in (0, r_0)$:
\begin{equation}
     \varphi^\prime (r) = \frac{1}{n \alpha(n)} \int_{\partial B(0,1)} u^\prime (x+ry) y dS(y).
\end{equation}
Inserting spherical coordinates and using the divergence theorem shows that $\forall r \in (0,r_0)$:
\begin{equation}
\varphi^\prime (r) = \frac{1}{n \alpha(n)r^{n-1}} \int_{\partial B(x,r)} u^\prime (z) \frac{z-x}{r} dS(y)
= \frac{1}{n \alpha(n)r^{n-1}} \int_{B(x,r)} \Delta u d V.
\end{equation}
Let $r \in (0, r_0)$. Then by continuity of $\Delta u$ together with the fact that $\alpha(n) r^n$ is the volume of $B(x,r)$:
\begin{equation}
 \varphi^\prime (r) = \underbrace{\frac{r}{n}}\_{\to 0 , \ r \to 0}  \underbrace{\frac{1}{\alpha(n) r^n}\int_{B(x,r)} \Delta u d V}_{ \to \Delta u (x), \ r \to 0}.
\end{equation}

And so $\varphi^\prime$ can be extended continuously to $0$ by $0$. This also shows item 3.
By Taylor's theorem
\begin{equation}
\frac{\varphi^{\prime \prime}(0)}{2} = \lim_{(0, r_0) \ni r \to 0 } \frac{1}{r^2} \bigg (\varphi (r) -\varphi (0)  - \varphi^\prime (0) r \bigg).
\end{equation}
Since $\varphi^\prime (0) =0$ item 4 follows from 3. $\square$

**Proposition 2 (harmonic functions have the mean value property):**
Let $u \in C^2(\Omega)$ with $\Delta u =0$. Then for all $x \in \Omega$ and $r \in (0, \infty)$ with $\bar B(x,r) \subset \Omega$:
\begin{equation}
    u (x) = \frac{1}{n \alpha(n)r^{n-1}} \int_{\partial B(x,r)} u dS.
\end{equation}
**Proof:**
This is an immediate consequence of proposition 1. $\square$

**Corollary:**
In the same situation:
\begin{equation}
    u(x) =  \frac{1}{ \alpha(n)r^{n}} \int_{B(x,r)} u dV.
\end{equation}

**Proof:**
Using spherical coordinates:
\begin{equation}
 \frac{1}{ \alpha(n)r^{n}} \int_{B(x,r)} u dV 
= \frac{1}{ \alpha(n)r^{n}} \int_0^r \int_{\partial B(x,\rho)} u dS d\rho.
\end{equation}
and so by the mean value property
\begin{equation}
  \frac{1}{ \alpha(n)r^{n}} \int_{B(x,r)} u dV 
=  \frac{1}{ \alpha(n)r^{n}}  u(x) n \alpha (n) \int_0^r  \rho^{n-1} d \rho 
= u(x). \quad \square
\end{equation}


**Proposition 3 (mean value property implies $C^\infty$ and harmonicity):**
Let $u \in C(\Omega)$ such that for all $x \in \Omega$ there is $r_0 \in (0, \infty)$ such that for all $r \in (0, r_0)$: $\bar B(0,r) \subset \Omega$ and
\begin{equation}
    \frac{1}{n \alpha(n) r^{n-1}} \int_{\partial B(x,r)} u dS = u(x).
\end{equation}
Then $u \in C^\infty (\Omega)$ and $\Delta u =0$.

**Proof:**
Let $\eta : \mathbb{R}^n \to \mathbb{R}$
\begin{equation}
    \eta (x):= c \begin{cases}
\exp \bigg ( \frac{1}{\\|x\\|^2 - 1} \bigg), \ \text{if} \ x \in B(0,1), \\\\ 
        0, \ \text{else}.
    \end{cases}
\end{equation}
With $c \in (0, \infty)$ chosen such that $\int_{\mathbb{R}^n} \eta dV = 1$.
Then $\eta \geq 0, \eta \in C^\infty (\mathbb{R}^n)$ and the support of $\eta$ is contained in $\bar B(0,1)$.
For $\varepsilon \in (0, \infty)$ define $\eta_\varepsilon : \mathbb{R}^n \to \mathbb{R}$ by
\begin{equation}
    \eta_\varepsilon (x) := \varepsilon^{-n} \eta ( x/\varepsilon).
\end{equation}
Then for all $\varepsilon \in (0, \infty)$: $\eta_\varepsilon \in C^\infty(\mathbb{R}^n)$, $\int_{\mathbb{R}^n} \eta_\varepsilon dV =1$ and the support of $\eta_\varepsilon$ is contained in $\bar B(0,\varepsilon)$.
For $\varepsilon \in (0, \infty)$ let $\Omega_\varepsilon := \\{ x \in \Omega : d(\partial \Omega, x) > \varepsilon\\}$ and $u_\varepsilon : \mathbb{R}^n \to \mathbb{R}$,
\begin{equation}
    u_\varepsilon  (x) := \int_{\bar \Omega_\varepsilon} \eta_\varepsilon(x-y) u(y) dV(y),
\end{equation}
where $u$ is extended by $0$ to $\mathbb{R}^n$. 
Let $\varepsilon \in (0, \infty)$:
Since $u$ is continuous on $\bar \Omega_\varepsilon$ the theorem of differentiation under the integral sign applies.
Therefore $u_\varepsilon \in C^\infty (\mathbb{R}^n)$.
Now let $x \in \Omega$ and $\varepsilon \in (0, \infty)$ such that $\varepsilon <r_0$.
In particular then $ \bar B(x,\varepsilon ) \subset \bar \Omega_\varepsilon$ and the support of $\eta_\varepsilon (x- \bullet)$ is contained in $\bar B(x, \varepsilon)$. Therefore
\begin{equation}
    u_\varepsilon (x) = 
 \int_{B(x, \varepsilon)} \eta_\varepsilon(x-y) u(y) dV(y).
\end{equation}
Inserting the definition of $\eta_\varepsilon$ and using spherical coordinates:
\begin{equation}
u_\varepsilon(x) = c \varepsilon^{-n} \int_0^\varepsilon \exp \bigg(\frac{1}{(r/\varepsilon)^2 -1} \bigg) \int_{\partial B(x,r)}u d S dr.
\end{equation}
Therefore (using the assumption on $u$, inserting the definition of $\alpha(n)$ and reverting the spherical coordinates)
\begin{equation}
    u_\varepsilon (x) = u(x) c   n \alpha(n) \int_0^\varepsilon  \exp \bigg(\frac{1}{(r/\varepsilon)^2 -1} \bigg) r^{n-1} dr = u(x)  \int_{\mathbb{R}^n} \eta_\varepsilon dV = u(x).
\end{equation}
This shows $u \in C^\infty (\Omega)$. Finally $\Delta u =0$ follows at once from item 4 in proposition 1. $\square$

**Corollary:**
Harmonic functions are $C^\infty$ and any partial derivative (of any order) of a harmonic function is harmonic (because the partial derivatives commute with the laplacian). Furthermore the local uniform limit of a sequence of harmonic functions is harmonic (since the limit satisfies the mean value property).

**Proposition 4 (strong maximum principle):**
Let $u \in C(\bar \Omega) \cap C^2(\Omega)$, $\Delta u=0$.
Then:
1. if $u$ attains its maximum in $\Omega$ then $u$ is constant,
2. \begin{equation}
    \max_{x \in \bar \Omega} u(x) = \max_{x \in \partial \Omega} u(x).
\end{equation}

**Proof:**
$\bar \Omega$ and $\partial \Omega$ are compact, because $\Omega$ is bounded (together with the Heine-Borel theorem).
Therefore $u$ attains its maximum.
To 1.:
Assume $u$ attains its maximum in $\Omega$.
Let
\begin{equation}
S:= \\{ x \in \Omega : u(x) = \max_{y \in \bar \Omega} u(y) \\}.
\end{equation}
Then $S \neq \varnothing$.
The idea is to show that $S$ is open and closed.
$S$ is closed being the preimage of a closed set (a singleton) by a continuous map.
Let $ x \in S$. Let $ r_0\in (0, \infty)$ such that $B(x,r_0) \subset \Omega$.
Let $r \in (0, r_0)$. Then
\begin{equation}
    0 = u(x) - \frac{1}{n \alpha(n) r^{n-1}} \int_{\partial B(x,r)} u dS
= \frac{1}{n \alpha(n) r^{n-1}} \int_{\partial B(x,r)} \underbrace{u(x) - u(y)}_{\geq 0} dS.
\end{equation}
Which implies that $u$ is constant on $\partial B(x,r)$.
Since $r$ was arbitrary it follows that $u$ is constant on $B(x,r_0)$ and so $S$ is open.
Therefore $S = \Omega$ and so $u$ is constant on $\Omega$ which in turn implies that $u$ is constant on $\bar \Omega$ by continuity.
To 2.: Follows from 1., because 2. is true if $u$ is constant and if not, then $u$ attains its maximum on $\partial \Omega$ by item 1. $\square$

**Proposition 5 (uniqueness of solution to the Dirichlet problem):**
Let $f \in C(\Omega)$ and $g \in C(\partial \Omega)$.
Then there exists at most one $u \in C(\bar \Omega) \cap C^2(\Omega)$ solving the Dirichlet problem:
\begin{equation}
    \begin{cases}
        - \Delta u = f \quad \text{on} \ \Omega, \\\\ 
u = g  \quad \text{on} \ \partial \Omega.
    \end{cases}
\end{equation}

**Proof:**
Let $u_1, u_2 \in C(\bar \Omega) \cap C^2(\Omega)$ be solutions to the Dirichlet problem.
Then $v := u_1 - u_2$ satisfies $\Delta v=0$ in $\Omega$ and $v = 0$ on $\partial \Omega$.
The function $-v$ satisfies the same.
Let $x \in \bar \Omega$.
By the maximum principle applied to $v$:
\begin{equation}
v(x) \leq \max_{y \in \bar \Omega} v(y) = \max_{y \in \partial \Omega} v(y) = 0.
\end{equation}
By the maximum principle applied to $-v$:
\begin{equation}
    -v (x) \leq  \max_{y \in \bar \Omega} -v(y) = \max_{y \in \partial \Omega} -v(y) = 0.
\end{equation}
Therefore $v(x) \geq 0$.
And so in total $0 \leq v(x) \leq 0$, which implies that $v(x) = 0$. $\square$

**Proposition 6:**
Let $u \in C^2(\Omega)$ with $\Delta u =0$.
Let $j \in \{1,\dots,n \}$.
Then for all $x \in \Omega$ and $r \in (0, \infty)$ such that $\bar B(x,r)\subset \Omega$:
\begin{equation}
    |\partial_j u(x)| \leq \frac{n}{r} \sup_{y \in \partial B(x,r)} |u(y)|.
\end{equation}

**Proof:**
By the corollary to the mean value property ($\partial_j u$ is harmonic by another corollary above) and the divergence theorem:
\begin{equation}
    \partial_j u(x) = \frac{1}{\alpha (n) r^{n}} \int_{B(x,r)} \partial_j u dV =
 \frac{1}{\alpha (n) r^{n}} \int_{\partial B(x,r)} u(y) \frac{y_j-x_j}{r} dS(y).
\end{equation}
and therefore
\begin{equation}
    |\partial_j u(x) | \leq  \frac{n}{r} \sup_{y \in \partial B(x,r)} |u(y)|. \quad \square
\end{equation}

**Proposition 7 (Liouvilles theorem):**
Let $u \in C^2(\mathbb{R}^n)$ with $\Delta u=0$ and $u$ bounded.
Then $u$ is constant.

**Proof:**
Let $j \in \{1,\dots,n \}$.
Let $x \in \mathbb{R}^n$. Then by the preceding proposition: $\forall r \in (0, \infty)$:
\begin{equation}
   |\partial_j u(x) |\leq \frac{n}{r} \sup_{y \in \mathbb{R}^n} |u(y)| \to 0 \  (r \to \infty).
\end{equation}
Therefore $u^\prime =0$ and so $u$ is constant. $\square$

**Proposition 8 (representation formula for bounded solutions of poisson problem in $\mathbb{R}^n$):**
Let $n \geq 3$.
Let $f \in C_c (\mathbb{R}^n)$ and $u \in C^2(\mathbb{R}^n)$ bounded with $-\Delta u = f$.
Then there exists $c \in \mathbb{R}$ such that for all $x \in \mathbb{R}^n$:
\begin{equation}
    u(x) = \int_{\mathbb{R}^n} \Phi(y) f(x-y) dV(y) +c,
\end{equation}
where $\Phi$ is the fundamental solution of poissons equation (see previous blog post).

**Proof:**
Let $v : \mathbb{R}^n \to \mathbb{R}$,
\begin{equation}
    v(x):=  \int_{\mathbb{R}^n} \Phi(x-y) f(y) dV(y).
\end{equation}
Then $v \in C^2 (\mathbb{R}^n)$ and $-\Delta v =f$ by the previous blog post.
Therefore it is left to show that $v$ is bounded. Because then $\Delta (u-v) =0$ and $u-v$ is bounded, so $u-v$ is constant by Liouvilles theorem.
Let $R\in (0, \infty)$ such that the support of $f$ is contained in $B(0,R)$.
Let $\varepsilon \in (0, \infty)$. Let $x \in \mathbb{R}^n$ with $\\|x\\| >2R$.
Then
\begin{equation}
    v(x)
=    \int_{B(0,R )} \Phi(x-y) f(y) dV(y). 
\end{equation}
Inserting the definition of $\Phi$:
\begin{equation}
|v(x)|
\leq  \int_{B(0,R )} |f(y)| \frac{1}{n(n-2) \alpha(n)}\frac{1}{\\|x-y\\|^{n-2}} dV(y)
\end{equation}
and so
\begin{equation}
  |v(x)|\leq \frac{1}{n(n-2) \alpha(n)}\frac{1}{R^{n-2}}  \int_{B(0,R )} |f| dV,
\end{equation}
since by the reverse triangle inequality for all $y \in B(0,R)$: $\\|x-y\\| \geq \\|x\\|- \\|y\\| \geq  2R - R =R$.
This shows that for all $x \in \mathbb{R}^n$:
\begin{equation}
    |v(x) | \leq \sup_{x \in \bar B(0,2R)} |v(x)| +  \frac{1}{n(n-2) \alpha(n)}\frac{1}{R^{n-2}}  \int_{B(0,R )} |f| dV
\end{equation}
and therefore $v$ is bounded. $\square$

**Proposition 8 (estimates for the partial derivatives):**
Let $u \in C^2(\Omega)$ with $\Delta u =0$ and $\alpha \in \mathbb{N}^n$.
Then for all $x \in \Omega$ and $r \in (0, \infty)$ such that $\bar B(x,r)\subset \Omega$.
\begin{equation}
    |D^\alpha u(x)| \leq \bigg(\frac{n |\alpha|}{r}\bigg)^{|\alpha|} \sup_{y \in B(x,r)} |u(y)|.
\end{equation}

**Proof:**
By induction on the order of the multi-index. Order $=1$ is the preceding proposition.
Let $k \in \mathbb{N}$, $k>0$ and assume the proposition holds for all multiindices of order $<k$.
Let $\alpha \in \mathbb{N}^n$ with $|\alpha| =k$.
Then $D^\alpha u $ is harmonic, because $u \in C^\infty$ and, because the partial derivatives commute.
Furthermore there exists $j \in \{1,\dots, n\}$ and $\beta \in \mathbb{N}^n$ with $|\beta| = k-1$ such that $D^\alpha u = \partial_j D^\beta u$.
Let $x \in \Omega$ and $r \in (0, \infty)$ such that $\bar B(x,r)\subset \Omega$.
By proposition 6:
\begin{equation}
    |D^\alpha u(x)| \leq \frac{n k}{r}\sup_{y \in \partial B(x,r/k)}| D^\beta u(x)|
\end{equation}
Let $y \in \partial B(x,r/k)$.
Then $B(y,r(k-1)/k) \subset B(x,r)$, since if $z \in B(y,r(k-1)/k)$, then
\begin{equation}
    \\| z-x \\| \leq \\| z-y\\| + \\|y-x\\| =  r (k-1)/k + r/k < r.
\end{equation}
Therefore by induction hypothesis
\begin{equation}
    |D^\beta u(y) | \leq \bigg(\frac{n (k-1)}{r (k-1)/k}\bigg)^{k-1} \sup_{z \in B(y,r(k-1)/k)} | u(z)|.
\end{equation}
and so in total
\begin{equation}
     |D^\alpha u(x)| \leq \bigg ( \frac{k }{r}\bigg)^k \sup_{z \in B(x,r)} |u(z)|. \quad \square
\end{equation}

**Proposition 9 (harmonic functions are analytic):**
Let $u \in C^2(\Omega)$ with $\Delta u =0$.
Then the Taylor series of $u$ is locally uniformly convergent to $u$.

**Proof:**
Let $x_0 \in \Omega$.
Let $r \in (0, \infty)$ such that $\bar B(x_0,r) \subset \Omega$.
For $k \in \mathbb{N}$ let $R_k: B(x_0,r) \to \mathbb{R}$
\begin{equation}
    R_k (x) := u(x) - \sum_{\alpha \in \mathbb{N}^n , |\alpha| = k} \frac{D^\alpha u(x_0)}{\alpha!} (x-x_0)^\alpha.
\end{equation}
Then for all $k \in \mathbb{N}$ and $x \in B(x_0,r)$ there is $t \in [0,1]$ with
\begin{equation}
    R_k(x) = \sum_{\alpha \in \mathbb{N}^n, |\alpha| = k+1} \frac{D^\alpha u(x_0 + t(x-x_0))}{\alpha !} (x-x_0)^\alpha
\end{equation}
by the Lagrange remainder formula.
Therefore by the multinomial theorem for all $k \in \mathbb{N}$, $\rho \in (0, r)$ and $x \in B(x_0,\rho)$:
\begin{equation}
    |R_k(x) |\leq \frac{\\| x-x_0\\|^{k+1}\_1}{(k+1)!}\max_{\alpha \in \mathbb{N}^n : |\alpha| = k+1} \sup_{x \in B(x_0, \rho)} | D^\alpha u (x)|.
\end{equation}
By the estimates for the partial derivatives for all $k \in \mathbb{N}^n$ (together with the triangle inequality):
\begin{equation}
 \max\_{\alpha \in \mathbb{N}^n : |\alpha| = k} \sup\_{ x \in \bar B(x_0,r/2) } | D^\alpha u (x)| \leq \bigg(\frac{n k}{r/2}\bigg)^{k} \underbrace{\sup\_{y \in B(x_0,r)} |u(y)|}\_{=:C}.
\end{equation}
Now let $\rho := r/(4 n^{3/2} e)$.
Then for all $k \in \mathbb{N}$ and $x \in B(x_0, \rho)$:
\begin{equation}
    |R_{k-1} (x)| \leq \frac{(\sqrt{n} \rho)^k}{k!} C\bigg(\frac{n k}{r/2}\bigg)^{k}
\leq  C  \bigg(\frac{r}{4n e}\bigg)^k \bigg(\frac{2 n e}{r}\bigg)^{k}
= C \frac{1}{2^k} \to 0 \ ( k \to \infty),
\end{equation}
where $ \\|\cdot \\|\_1 \leq \sqrt{n} \\| \cdot \\|\_2$ and $k^k /k! \leq e^k$ (by the exponential series) was used. $\square$

**Proposition 10 (Harnack's inequality):**
For every domain $V \subset \Omega$  with $\bar V \subset \Omega$ there exists $C \in (0, \infty)$ such that for all $u \in C^2(\Omega)$ with $u\geq 0$ and $\Delta u =0$:
\begin{equation}
    \sup_{x \in V} u(x) \leq C \inf_{x \in V} u.
\end{equation}
**Proof:**
Let $y \in \Omega$ and $r \in (0,\infty)$ such that $B(y,4r) \subset \Omega$.
Let $x_1, x_2 \in B(y,r)$.
Then using the mean value property, $u \geq 0$ and $B(x_1,r) \subset B(x_2,3r) \subset B(y,4r)$:
\begin{equation}
\begin{split}
    u(x_1) &= \frac{1}{\alpha(n) r^n} \int_{B(x_1,r)} u dV \leq  \frac{1}{\alpha(n) r^n} \int_{B(x_2,3r)} u dV \\\\ 
&=  \frac{3^n}{\alpha(n) (3r)^n} \int_{B(x_2,3r)} u dV = 2^n u(x_2).
\end{split}
   \end{equation}
Finally let $a,b \in V$ arbitrary.
Let $\gamma :[0,1]\to V$ continuous with $\gamma (0) = a, \gamma (1) = b$ (exists by connectedness).
Let $\rho \in (0, \infty)$ such that $\forall x \in \bar V$: $B(x,4 \rho) \subset \Omega$ (exists since $\bar V \subset \Omega$ is compact).
Since $\gamma$ is uniformly continuous there exists $\delta >0$ such that for all $ t ,s \in [0,1]$:
\begin{equation}
    |t-s |< \delta \Rightarrow \\|\gamma (t) -\gamma (s)\\| < \rho.
\end{equation}
Let $t_0, \dots, t_N \in [0,1]$ with $0=t_0 < \cdots < t_N =1$ with for all $t \in \\{0, \dots, N-1\\}$: $t_{j+1}- t_j < \delta$. 
Let $j \in \\{1,\dots, N-1\\}$.
Then $t_{j+1}  - t_j < \delta$ and $ t_j -t_{j-1} < \delta$. Therefore $\gamma(t_{j+1})$ and $\gamma(t_{j-1})$ are in $B(\gamma(t_j), \rho)$.
Therefore the first part of the argument applies to show that
\begin{equation}
    u(\gamma(t_{j-1})) \leq  2^n u ( \gamma(t_{j+1})).
\end{equation}
Since $j$ was arbitary iterative application yields:
\begin{equation}
    u(a) = u(\gamma(t_0)) \leq 2^{nN} u(\gamma (t_N)) = 2^{nN} u(b). \quad \square
\end{equation}

**Proposition 11 (Harnack's convergence theorem)**: 
Let $(u_m)\_{m \in \mathbb{N}}$ be a point-wise non-decreasing sequence of harmonic functions in $\Omega$. 
Let $u : \Omega \to (0, \infty]$ be the point-wise limit. 
Then either $u = \infty$ or $u$ is never infinite and $(u_m)_{m \in \mathbb{N}}$ is converging locally uniformly to $u$ (and therefore $u$ is harmonic).

**Proof:**
Let $x_0 \in \Omega$ such that $u(x_0) <\infty$.
Let $x \in \Omega$.
Let $V \subset \Omega$ a region with $\bar V \subset \Omega$, $x_0,x \in V$.
The existence of $V$ follows by taking a union of balls along a continuous curve connecting $x_0$ with $x$ (similar to the proof of Harnack's inequality).
Let $C \in (0, \infty)$ be the constant from Harnack's inequality associated to $V$.
Let $\varepsilon \in (0, \infty)$.
Let $N \in \mathbb{N}$ such that for all $m,k \in \mathbb{N}$ with $m\geq k \geq N$: 
$ u_m(x_0)- u_k (x_0)< \varepsilon$ (possible since $\lim_{m \to \infty} u_m (x_0) \in \mathbb{R}$ and convergent sequences are Cauchy).
Then by Harnack's inequality for all $k,m\in \mathbb{N}$ with $m>k\geq N$ and $y \in V$:
\begin{equation}
   |u_m (y) - u_k(y)| =  (u_m - u_k)(y)  \leq C (u_m (x_0) - u_k(x_0))< \varepsilon.
\end{equation}
Therefore $u$ is real valued in $\bar V$ and $(u_m)_{m \in \mathbb{N}}$ is a Cauchy sequence in $C(\bar V)$ and therefore uniformly convergent to $u$ in $\bar V$. $\square$
