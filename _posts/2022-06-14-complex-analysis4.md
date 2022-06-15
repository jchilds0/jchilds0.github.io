---
title: Denjoy-Wolff Theorem (4/6)
date: 2022-06-14 13:00
categories: [Complex Analysis, Holomorphic Dynamics and Möbius Transformations]
tags: [möbius transformations, algebraic semigroups]     # TAG names should always be lowercase
math: true
comments: false
---

[//]: <> (Convert Latex to Markdown, Add newlines to seperate equations)
[//]: <> (pandoc EulerIdentity.tex -o test1.md --mathml)

# Julia's Lemma

This section follows chapter 1.4 of [4]. In this section we prove Julia's lemma, a more general theorem than the
Denjoy Wolff theorem, which we will use to prove the Denjoy Wolff
theorem. The main type of set we will be dealing with throughout this
chapter is called a horocycle.

**Definition**
Let $\tau \in \partial \mathbb{D}$, and $R > 0$. The horocycle $E(\tau, R)$ is,

$$E(\tau, R) = \{ z \in \mathbb{D} \ | \ \frac{|\tau - z|^2}{1 - |z|^2} < R \}$$

$E(\tau, R)$ is an open Euclidean disk tangent to the unit disk at
$\tau$ of radius $R / (R + 1)$. To begin we prove a property of points
inside a horocycle.

**Proposition**
$z \in E(\tau, R)$ iff

$$\liminf_{w \to \tau} d_\mathbb{D} (z, w) - d_\mathbb{D} (0, w) < \ln R$$

**Prove**
Let $z \in \mathbb{D}$, firstly we use $T_z$ to map $z \to 0$ and then apply
**Example 3.1**.

$$\begin{aligned}
d_\mathbb{D} (z, w) - d_\mathbb{D} (0, w) &= d_\mathbb{D} (0, T_z (w)) - d_\mathbb{D} (0, w) \\
&= \ln \bigg( \frac{1 + |T_z ( w )|}{1 - |T_z (w)|} \bigg) - \ln \bigg( \frac{1 + |w|}{1 - |w|} \bigg) \\
&= \ln \bigg( \frac{1 - |w|}{1 - |T_z (w)|} \bigg) - \ln \bigg( \frac{1 + |w|}{1 + |T_z ( w )|} \bigg)
\end{aligned}$$

Since $\|w\| \to 1$ as $w \to \tau$,

$$\lim_{w \to \tau} \ln \bigg( \frac{1 + |w|}{1 + |T_z ( w )|} \bigg) = 0$$

This allows us to replace the minus sign above with a positive one,

$$\begin{aligned}
\liminf_{w \to \tau} d_\mathbb{D} (z, w) - d_\mathbb{D} (0, w) &= \liminf_{w \to \tau} \ln \bigg( \frac{1 - |w|}{1 - |T_z (w)|} \bigg) + \ln \bigg( \frac{1 + |w|}{1 + |T_z ( w )|} \bigg) \\
&= \liminf_{w \to \tau} \ln \bigg( \frac{1 - |w|^2}{1 - |T_z (w)|^2} \bigg)
\end{aligned}$$

Simplifying the argument of the logarithm,

$$\begin{aligned}
\frac{1 - |w|^2}{1 - |T_z (w)|^2} &= (1 - |w|^2) \frac{|1 - \bar{z} w|^2}{|1 - \bar{z} w|^2 - |z - w|^2} \\
&= \frac{(1 - |w|^2)|1 - \bar{z} w|^2}{1 - 2 \Re(\bar{z} w) + |z|^2 |w|^2 - (|z|^2 - 2 \Re(\bar{z} w) + |w|^2)} \\
&= \frac{(1 - |w|^2)|1 - \bar{z} w|^2}{(1 - |w|^2)(1 - |z|^2)} \\
&= \frac{|1 - \bar{z} w|^2}{1 - |z|^2} \\
&= \frac{|\bar{w} - |w|^2 \bar{z}|^2}{|w|^2(1 - |z|^2)} \\
&= \frac{|w - |w|^2 z|^2}{|w|^2(1 - |z|^2)}
\end{aligned}$$

Since $\|w\| \to 1$ as $w \to \tau$,

$$\liminf_{w \to \tau} d_\mathbb{D} (z, w) - d_\mathbb{D} (0, w) = \ln \bigg(\frac{|\tau - z|^2}{1 - |z|^2} \bigg)$$

So the proposition follows from the definition of a horocycle.

The next notion we need is called the boundary dilation coefficient
which measures how quickly $\varphi$ moves points towards $\sigma$.

**Definition**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic and $\sigma \in \partial \mathbb{D}$, then

$$\alpha_\varphi (\sigma) = \liminf_{z \to \sigma} \frac{1 - |\varphi(z)|}{1 - |z|}$$

is the boundary dilation coefficient.

Similarly to the horocycle, we prove a property of the boundary dilation
coefficient.

**Proposition**
$$\liminf_{w \to \sigma} d_\mathbb{D} (0, w) - d_\mathbb{D} (0, \varphi(w)) = \ln \alpha_\varphi (\sigma)$$

**Proof**
Using **Example 3.1**,

$$\begin{aligned}
d_\mathbb{D} (0, w) - d_\mathbb{D} (0, \varphi(w)) &= \ln(\frac{1 + |w|}{1 - |w|}) - \ln(\frac{1 + |\varphi(w)|}{1 - |\varphi(w)|}) \\
&= \ln \bigg( \frac{1 - |\varphi(w)|}{1 - |w|} \bigg) + \ln \bigg( \frac{1 + |w|}{1 + |\varphi(w)|} \bigg)
\end{aligned}$$

Therefore,

$$\liminf_{w \to \sigma} d_\mathbb{D} (0, w) - d_\mathbb{D} (0, \varphi(w)) = \ln \alpha_\varphi (\sigma)$$

The final proposition we need before we can prove Julia's Lemma involves
a property of the hyperbolic metric.

**Proposition**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic, then $\varphi$ contracts
distances with respect to the hyperbolic metric $d_\mathbb{D}$. Namely,

$$d_\mathbb{D} ( \varphi(u), \varphi(v)) \leq d_\mathbb{D} (u, v)$$

for $u, v \in \mathbb{D}$. Equality occurs iff $\varphi$ is an automorphism of
the unit disk

**Proof**
Equality follows from the construction of $d_\mathbb{D}$,

$$\begin{aligned}
d_\mathbb{D} (\varphi(u), \varphi(v)) &= d_\mathbb{D} (0, T_{\varphi(u)} (\varphi(v))) \\
&= \ln \bigg( \frac{1 + |T_{\varphi(u)} (\varphi(v))|}{1 - |T_{\varphi(u)} (\varphi(v))|} \bigg) \\
\text{By the Schwarz Pick Lemma}
&\leq \ln \bigg( \frac{1 + |T_u(v)|}{1 - |T_u(v)} \bigg) \\
&= d_\mathbb{D} (u, v)
\end{aligned}$$

**Theorem**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic and $\sigma \partial \mathbb{D}$.
Assume $\alpha_\varphi (\sigma) < \infty$, then there exists
$\eta \in \mathbb{D}$ such that for all $R > 0$,
$$\varphi(E(\sigma, R)) \subset E(\eta, \alpha_\varphi(\sigma) R)$$

**Proof**
Since $\alpha_\varphi (\sigma) < \infty$ we can find a sequence
$(w_1, w_2, ...)$ converging to $\sigma$ such that,

$$\lim_{k \to \infty} \frac{1 - |\varphi(w_k)|}{1 - |w_k|} = \alpha_\varphi(\sigma)$$

Using **Prop 7.0.2**,

$$\lim_{k \to \infty} d_\mathbb{D} (0, w_k) - d_\mathbb{D} (0, \varphi(w_k)) = \ln \alpha_\varphi(\sigma)$$

Let $\eta = \lim_{k \to \infty} \varphi(w_k)$ and $z \in E(\sigma, R)$. We want to show that $\varphi(z) \in
E(\eta, \alpha_\varphi(\sigma) R)$. By **Prop 7.0.1** this is equivalent to

$$\lim_{k \to \infty} d_\mathbb{D} (\varphi(z), \varphi(w_k)) - d_\mathbb{D} (0, \varphi(w_k)) < \ln \alpha_\varphi(\sigma) R$$

By **Prop 7.0.3**,

$$\begin{aligned}
d_\mathbb{D} (\varphi(z), \varphi(w_k)) - d_\mathbb{D} (0, \varphi(w_k)) &< d_\mathbb{D} (z, w_k) - d_\mathbb{D} (0, \varphi(w_k)) \\
&= d_\mathbb{D} (z, w_k) - d_\mathbb{D} (0, w_k) + d_\mathbb{D} (0, w_k) - d_\mathbb{D} (0, \varphi(w_k))
\end{aligned}$$

By **Prop 7.0.1**, $z \in E(\sigma, R)$ is equivalent to

$$\lim_{k \to \infty} d_\mathbb{D} (z, w_k) - d_\mathbb{D} (0, w_k) < \ln R$$

By **Prop 7.0.2**, $d_\mathbb{D} (0, w_k) - d_\mathbb{D} (0, \varphi(w_k)) \to \ln \alpha_\varphi (\sigma)$
as $k \to \infty$. Therefore,

$$\lim_{k \to \infty} d_\mathbb{D} (\varphi(z), \varphi(w_k)) - d_\mathbb{D} (0, \varphi(w_k)) < \ln R + \ln \alpha_\varphi (\sigma)$$

and,

$$\varphi(E(\sigma, R)) \subset E(\eta, \alpha_\varphi(\sigma) R)$$

# Denjoy-Wolff Theorem

This section follows chapter 1.8 of [4]. The following proposition and Denjoy-Wolff Theorem will allow us to give
an generalisation of the classification developed in the previous
chapter on Möbius Transformations.

**Proposition**
Let $\phi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic, not an automorphism. Suppose
there exists $\tau \in \mathbb{D}$ such that $\phi(\tau) = \tau$. Then
${ \phi^{\circ n} }$ converges uniformly on compacta to the constant map
$z \mapsto \tau$.

**Proof** [4]
Firstly suppose $\phi(0) = 0$. Then by the Schwarz lemma we have that
$| \phi(z) | \leq |z|$. Let $0 < r < 1$ and
$M(r) = \max_{|z| \leq r} {|\phi(z)|}$. Let $\delta = M(r) / r > 0$. The
previous note ensures $\delta < 1$. Let $\psi = \frac{\phi(rz)}{M(r)}$.
Clearly $\psi$ fixes $0$ and is holomorphic on $\mathbb{D}$. Since
$r \in (0, 1)$, $\psi$ is continuous on $\overline{\mathbb{D}}$. Thus by the
Schwarz lemma $| \psi(z) | \leq |z|$, which implies that,

$$|\phi(z)| = M(r) \big| \psi \big( \frac{z}{r} \big) \big| \leq \frac{M(r)}{r} |z| \leq \delta |z|$$

Thus by induction we have
$| \phi^{\circ n} (z) | \leq \delta^n |z| \leq \delta^n$. Since
$\delta < 1$, $\phi^{\circ n}$ tends to 0 uniformly on $r \overline{\mathbb{D}}$
and since $r$ was arbitrary, ${ \phi^{\circ n} }$ converges uniformly to
$0$ on compact subsets of $\mathbb{D}$.

If $\tau \neq 0$ then we apply the previous argument to
$\varphi = T_\tau \circ \phi \circ T_\tau$. Then $\varphi$ is
holomorphic, not an automorphism and thus $\varphi^{\circ n}$ converges
to $0$ uniformly on compacta. Hence
$\phi^{\circ n} = T_\tau \circ \varphi^{\circ n} \circ t_\tau$ converges
uniformly on compacta to $T_\tau (0) = \tau$.

Before we state the Denjoy Wolff Theorem, we make some remarks about
Möbius Transformations.

Let $T$ be a parabolic transformation in $\mathbb{H}$. We found that one
could conjugate this transform using another automorphism $D$ which
takes the fixed point of $T$ to $\infty$. Then $D \circ T \circ D^{-1}$
is a parabolic transformation with a fixed point at $\infty$ and thus a
translation. So $(D \circ T \circ D^{-1})^{\circ n} (z) \to \infty$ as
$n \to \infty$ and thus $T^{\circ n}$ converges uniformly on compacta to
$z \mapsto p$ where $p$ is the fixed point of $T$.

Similarly let $T$ be a hyperbolic transformation, and $D$ be an
automorphism conjugating the fixed points of $T$ to $0$ and $\infty$.
Then $D \circ T \circ D^{-1}$ is a hyperbolic transformation with fixed
points at $0$ and $\infty$ and thus a dilation. So
$(D \circ T \circ D^{-1})^{\circ n} (z) \to \infty$ (or $0$ depending on
the magnitude of the dilation) as $n \to \infty$ and thus $T^{\circ n}$
converges uniformly on compacta to $z \mapsto p$ where $p$ is a fixed
point of $T$ (the fixed point corresponding to $0$ or $\infty$, which
depends on the previous statement). We are now ready to state the Denjoy
Wolff Theorem.

**Theorem**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic and assume $\varphi$ has no
fixed points in $\mathbb{D}$. Then there exists $\tau \in \partial \mathbb{D}$ unique
such that $\alpha_\varphi (\tau) \leq 1$ and for every $R > 0$,
$$\varphi(E(\tau, R)) \subset E(\tau, R)$$

**Proof** [4]
Firstly for each $z \in \mathbb{D}$, the sequence $|\varphi^{\circ n} (z)|$
converges to 1. Suppose not, then there exists a subsequence $n_k$ such
that $\lim_{k \to \infty} \varphi^{ \circ n_k} (z) = p \in \mathbb{D}$. Since
elliptic transformation have fixed points in $\mathbb{D}$ and from the previous
discussion on uniform convergence, $\varphi$ is not an automorphism. By
**Proposition 7.0.3**, the map
$\mathbb{N} \ni n \mapsto d(\varphi^{\circ n} (z_0), \varphi^{\circ (n + 1)}(z_0))$
is decreasing and thus converges. Since
$p = \lim_{k \to \infty} \varphi^{ \circ n_k} (z)$,

$$\begin{aligned}
d(p, \varphi(p)) &= \lim_{k \to \infty} d(\varphi^{\circ n_k} (z_0), \varphi^{\circ (n_k + 1)}(z_0)) \\
&= \lim_{k \to \infty} d(\varphi^{\circ n_k + 1} (z_0), \varphi^{\circ (n_k + 2)}(z_0)) \\
&= d( \varphi(p), \varphi^{\circ 2} (p))
\end{aligned}$$

Since $\varphi$ is not an automorphism, this is only possible if
$\varphi(p) = p$, a contradiction. Therefore, for every $z \in \mathbb{D}$,
$\varphi^{\circ n} (z)$ accumulates on the boundary of $\mathbb{D}$. Let
$(w_n)\_{n \in \mathbb{N}}$ be a sequence defined by
$w\_{n + 1} = \varphi(w_n)$ and $w_1 = 0$. Since
$\lim_{n \to \infty} |w_n| = 1$, there exists a subsequence $n_k$ such
that $|\varphi(w_{n_k})| > |w_{n_k}|$. Thus up to extracting a
converging subsequence, we can assume $w_{n_k}$ converges to
$\tau \in \mathbb{D}$. By construction, $\varphi(w_{n_k})$ also converges to
$\tau$. Since $|\varphi(w_{n_k})| \geq |w_{n_k}|$, then
$1 - |\varphi(w_{n_k})| < 1 - |w_{n_k}|$ and thus,

$$\alpha_\varphi(\sigma) = \lim_{n \to \infty} \frac{1 - |\varphi(w_n)}{1 - |w_n|} \leq 1$$

Therefore by Julia's Lemma, for all $R > 0$

$$\varphi( E(\tau, R)) \subset E(\tau, R)$$

Suppose there exists $\tau' \in \mathbb{D}$ that also satisfies the above formula. Let
$R, R' \in \mathbb{R}$ such that
$\overline{E(\tau, R)} \cap \overline{E(\tau', R')} = { z_0 }$, $R$ and
$R'$ exists and are well defined as $E$ is an open disk in $\mathbb{R}^2$. Thus,

$$\begin{aligned}
\varphi({z_0}) &= \varphi(\overline{E(\tau, R)} \cap \overline{E(\tau', R')}) \\
&= \varphi(\overline{E(\tau, R)}) \cap \varphi(\overline{E(\tau', R')}) \\
\text{Since $ \varphi $ is continuous,} \\
&\subset \overline{\varphi(E(\tau, R))} \cap \overline{\varphi(E(\tau', R'))} \\
&\subset \overline{E(\tau, R)} \cap \overline{E(\tau', R')} \\
&= { z_0 }
\end{aligned}$$

Which is a contradiction, $z_0 \in \mathbb{D}$ and $\varphi$ has no fixed points
in $\mathbb{D}$. Therefore $\tau$ is unique.

Finally we show that $\varphi$ converges uniformly on compacta to
$z \mapsto \tau$. By Vitali's Theorem [9], it suffices to show
$\lim_{n \to \infty} \varphi^{\circ n}(z_0) = \tau$. Let $z_0 \in \mathbb{D}$.
Then there exists $R > 0$ such that $z_0 \in E(\tau, R)$. By construction,
$\varphi^{\circ n} (z_0) \in E(\tau, R)$. Since
$\varphi^{\circ n} (z_0)$ accumulates on $\partial \mathbb{D}$ and
$\overline{E(\tau, R)} \cap \partial \mathbb{D} = { \tau }$,
$\lim_{n \to \infty} \varphi^{\circ n}(z_0) = \tau$.

**Definition**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic, not the identity.

1.  If $\varphi$ has a fixed point in $\mathbb{D}$, then its unique fixed point
    is called the *Denjoy-Wolff point* of $\varphi$.

2.  If $\varphi$ has no fixed points in $\mathbb{D}$, then the unique point
    $\tau \in \partial \mathbb{D}$ given by the Denjoy-Wolff Theorem is the
    *Denjoy-Wolff point* of $\varphi$

Moreover, $\varphi$ is

1.  *elliptic* if its Denjoy-Wolff point is in $\mathbb{D}$,

2.  *hyperbolic* if its Denjoy-Wolff point $\tau$ belongs to
    $\partial \mathbb{D}$ and $\alpha_\varphi (\tau) \in (0, 1)$,

3.  *parabolic* if its Denjoy-Wolff point $\tau$ belongs to
    $\partial \mathbb{D}$ and $\alpha_\varphi (\tau) = 1$.

This definition generalizes the classification made in the previous
chapter from automorphisms to holomorphic self maps.
