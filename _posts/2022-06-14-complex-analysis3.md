---
title: Möbius Transformations (3/6)
date: 2022-06-14 12:00
categories: [Complex Analysis, Holomorphic Dynamics and Möbius Transformations]
tags: [möbius transformations, algebraic semigroups]     # TAG names should always be lowercase
math: true
comments: false
---

[//]: <> (Convert Latex to Markdown, Add newlines to seperate equations)
[//]: <> (pandoc EulerIdentity.tex -o test1.md --mathml)

# Classification

To motivate our classification, we examine the fixed points of a Möbius transformation. Let $\varphi$ be a Möbius
transformation with coefficients given by $A = \begin{pmatrix}  a & b \\ c & d \end{pmatrix} \in \text{PSL}(2, \mathbb{R})$. A
fixed point of $\varphi$ is a point $z \in \mathbb{C}$ such that $\varphi(z) = z$, thus

$$\begin{aligned}
z &= \frac{az + b}{cz + d} \\
z(cz + d) &= az + b \\
0 &= cz^2 + (d - a) z - b\end{aligned}$$ $$\begin{aligned}
\Delta &= (a - d)^2 + 4bc \\
&= (a - d)^2 + 4(ad - 1) \\
&= (a + d)^2 - 4\end{aligned}$$

Thus since $a, d$ are real, we get two real fixed points when
$(a + d)^2 > 4$, one fixed point when $(a + d)^2 = 4$ and two complex
fixed points when $(a + d) \in [0, 4)$.

A useful property of the trace is given by the following,

**Proposition**
Let $D, B \in \text{SL}(2, \mathbb{R})$, then

$$\text{tr} D B D^{-1} = \text{tr} B$$

**Proof**
Let $A \in \text{SL}(2, \mathbb{R})$ and $B \in \text{SL}(2, \mathbb{R})$, then the $\text{tr} AB$ is the
sum of the eigenvalues of $AB$, which is given by the characteristic
polynomial,

$$\begin{aligned}
\det(BA - \lambda I) &= \det(B^{-1} (BA - \lambda I) B) \\
&= \det(AB - \lambda I) \\
&= 0
\end{aligned}$$

Thus $AB$ and $BA$ have the same eigenvalues and therefore $\text{tr} AB = \text{tr} BA$.

Let $D, B \in \text{SL}(2, \mathbb{R})$, then
$\text{tr}(D B D^{-1}) = \text{tr}((DB)D^{-1}) = \text{tr}(D^{-1} (DB)) = \text{tr} B$

## Parabolic

**Definition**
A Möbius transformation $\varphi$ is Parabolic if $\varphi$ has one
fixed point.

Equivalently, $(a + d)^2 = 4$. We note that since the coefficients are
real, the fixed point lies on the boundary of $\mathbb{H}$. An example
of a parabolic transformation is the translation $z \to z + 2$ in
$\mathbb{H}$. Geometrically parabolic transformations are translations
in the upper half complex plane, more specifically they're translation
around a horoball at the fixed point.

**Definition**
Let $p$ be a point on the boundary of $\mathbb{H}$, Let $C_p$ be a
Euclidean circle tangent to the boundary at $p$. Then the region bound
by $C_p$ is a horoball at $p$, denoted $H_p$. Note if $p$ is the point
at $\infty$ then $C_\infty$ is a horizontal line and $H_\infty$ is the
Euclidean half plane above $C_\infty$

**Proposition**
Let $A(z) = z + a$, for $a \in \mathbb{R}$. Then $A$ fixes $H_\infty$.

This follows from the definition of $H_\infty$, now we generalise this
proposition to arbitrary hyperbolic transformations.

**Theorem**
Let $\varphi$ be a parabolic Möbius transformation with a fixed point
$p$. Then $H_p$ is invariant under $\varphi$

**Proof** [7]
Let $D = \frac{-1}{z - p}$, $D$ conjugates $B$ to $A$, namely,
$A(z) = DBD^{-1}(z)$. By **Prop 6.0.1**, $A$ is also a parabolic
transformation, with a fixed point at infinity and thus fixes
$H_\infty$. Let $H_\infty$ be a horoball with
$\partial H_\infty = \{ z \in \mathbb{C} \ | \ \Im(z) = t_0 \}$. $D^{-1}$ maps
$\partial H_\infty$ to $C_p$ and $\mathbb{R}$ to $\mathbb{R}$. Since $\partial H_\infty$
and $\mathbb{R}$ are tangent at $\infty$, $C_p$ is tangent to $\mathbb{R}$ at $p$.
Therefore $H_p = D^{-1} (H_\infty)$ is a horoball at $p$, and since $A$
leaves $H_\infty$ invariant, we conclude that $B$ leaves $H_p$
invariant.

**Example**
Let $\varphi : \mathbb{H} \mapsto \mathbb{H}$ be defined by

$$\varphi(z) = \frac{2z - 1}{z}$$

$\varphi$ is parabolic since $(\text{tr} \varphi)^2 = 4$.

<iframe width=720 height=400 src="/assets/report/types/Parabolic,%20z%20=%20(2z%20-%201)%20div%20z.mp4" frameborder="0" allowfullscreen></iframe>

## Elliptic

**Definition**
A Möbius transformation $\varphi$ is Elliptic if $\varphi$ has two
complex fixed points.

Equivalently, $(a + d)^2 \in [0, 4)$. Since the coefficients are real,
we cannot have one complex root. Applying the conjugate root theorem, we
have one fixed point in $\mathbb{H}$ and the other is outside
$\mathbb{H}$. Geometrically elliptic transformations are rotations
around the fixed point.

**Example**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be defined by

$$\varphi(z) = iz$$

$\varphi$ is elliptic since it has one fixed point in $\mathbb{D}$.

<iframe width=720 height=400 src="/assets/report/types/Elliptic,%20a%20=%200,%20t%20=%20pi%202.mp4" frameborder="0" allowfullscreen></iframe>

## Hyperbolic

**Definition**
A Möbius transformation $\varphi$ is Hyperbolic if $\varphi$ has two
distinct real fixed points.

Equivalently, $(a + d)^2 > 4$. An example of a hyperbolic transformation
is the dilation $z \to 2z$ in $\mathbb{H}$. Geometrically hyperbolic
transformations are dilations in the upper half complex plane.

**Proposition**
Let $A(z) = \lambda z$ for $\lambda > 1$ and define,

$$\ell (A) = \inf_{z \in \mathbb{H}} d_\mathbb{H} (z, A(z))$$

Then $\inf$ is achieved for $z \in \Im$.

**Proof** [7]
Let $z \in \mathbb{H}$. The radial projections of $z$ and $A(z)$ onto
the imaginary axis are $|z| i$ and $\lambda |z| i$. Let
$\phi_p(w) = \frac{w - p}{w - \bar{p}}$. $\phi_p$ maps the upper half
plane to the unit disk sending $p \to 0$.

$$\begin{aligned}
d_{\mathbb{H}}(z, \lambda z) &= d_\mathbb{D} \bigg(0, \frac{(\lambda - 1) z}{\lambda z - \bar{z}} \bigg) \\
&= \ln \frac{1 + \frac{|(\lambda - 1) z|}{|\lambda z - \bar{z}|}}{1 - \frac{|(\lambda - 1) z|}{|\lambda z - \bar{z}|}} \\
&= \ln \frac{|\lambda z - \bar{z}| + |(\lambda - 1) z|}{|\lambda z - \bar{z}| - |(\lambda - 1) z|} \\
&\geq \ln \frac{|\lambda z| + |\bar{z}| + |(\lambda - 1) z|}{|\lambda z| + |\bar{z}| - |(\lambda - 1) z|} \\
&= \ln \lambda \\
&= d_\mathbb{H} (i, \lambda i) \\
&= d_\mathbb{H} (|z|i, \lambda |z| i)
\end{aligned}$$

Therefore the distance between $z$ and $\lambda z$ has a minimum of the
distance between their radial projections onto the imaginary axis.
Equality occurs when $|\lambda z - \bar{z}| = |\lambda z| + |\bar{z}|$.

$$\begin{aligned}
|\lambda z - \bar{z}|^2 &= \lambda^2 |z|^2 - 2 \lambda \Re{z^2} + |\bar{z}|^2 \\
(|\lambda z| + |\bar{z}|)^2 &= (\lambda + 1)^2 |z|^2 \\
\Re(z^2) &= |z|^2
\end{aligned}$$

Therefore $\Re(z) = 0$, so the minimum is achieved on the imaginary
axis.

**Theorem**
Let $B$ be a hyperbolic Möbius transformation with fixed points $(u, v)$
and $L(t)$ be the geodesic in $\mathbb{H}$ between $u$ and $v$. Then
$\ell(B)$ achieves a minimum iff $z \in \ell(B)$

**Proof** [7]
We can assume $u > v$. Let $D(z) = \frac{z - u}{z - v}$, then $D$ takes
the fixed points of $B$, $u$, $v$ to $0$ and $\infty$ respectively. $D$
is also an isometry of $\mathbb{H}$ and maps $L$ to $\Im$. Thus we have
$B D B^{-1} (z) = \lambda z$ for some $\lambda > 0$, so we apply the
previous proposition to $B D B^{-1}$ if $\lambda > 1$ and
$B D^{-1} B^{-1}$ if $\lambda < 1$. Since the identity is not
hyperbolic, $\lambda \neq 1$.

**Example**
Let $\varphi : \mathbb{H} \mapsto \mathbb{H}$ be defined by

$$\varphi(z) = 2z$$

$\varphi$ is parabolic since $(\text{tr} \varphi)^2 = 9$.

<iframe width=720 height=400 src="/assets/report/types/Hyperbolic,%20z%20=%202z.mp4" frameborder="0" allowfullscreen></iframe>
