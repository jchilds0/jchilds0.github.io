---
title: Poincare Disk (1/6)
date: 2022-06-14 10:00
categories: [Complex Analysis, Holomorphic Dynamics and Möbius Transformations]
tags: [möbius transformations, algebraic semigroups]     # TAG names should always be lowercase
math: true
comments: false
---

[//]: <> (Convert Latex to Markdown, Add newlines to seperate equations)
[//]: <> (pandoc EulerIdentity.tex -o test1.md --mathml)

The following series is a transcription of my final report from MTH3000, a Monash University third year maths research project.
The full report as a pdf is available here [MTH3000 - Report](/assets/report/MTH3000_Report.pdf)

# Introduction

## History

A brief history of the concepts that will be developed in this report.
The two spaces we are interested in are known as the Poincaré disk and
Poincaré half-space or upper half plane. Both of these are named after
Henri Poincaré, but it was originally developed by Eugenio Beltrami who
used it to show that hyperbolic geometry was equiconsistent with
Euclidean geometry [8]. A natural question that arises in the
study of models concerns the automorphisms of that space, and in the
case of the upper half plane, these turn out to be the Möbius
transformations. Möbius transformations were developed by August
Ferdinand Möbius around 1827 during his study of analytical geometry. A
group we will see later called the projective special linear group,
which is very closely related to Mobius transformations, was developed
by Evariste Galois in the 1830s, in the context of Lie Groups.
Continuous one-parameter semigroups of holomorphic self-maps of the unit
disc $\mathbb{D}$ in the complex plane $\mathbb{C}$ have been studied since the early
1900s, both for their intrinsic interest in complex analysis and for
1900s, both for their intrinsic interest in complex analysis and for
applications to areas such as differential equations [4].

## Complex Analysis

To begin we state some standard definitions in complex analysis.

**Definition**
Let $z = x + iy \in \mathbb{C}$ for $x, y \in \mathbb{R}$, and
$f(x, y) = u(x, y) + i v(x, y)$. The Cauchy-Riemann Equations are given
by,

$$ \frac{\partial u}{\partial x} = \frac{\partial v}{\partial y} \qquad \frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}$$

**Definition**
A map $f : U \subset \mathbb{C} \mapsto \mathbb{C}$ is *holomorphic* if it satisfies the
Cauchy Riemann Equations on $U$

**Definition**
A map $f : U \subset \mathbb{C} \mapsto \mathbb{C}$, is *biholomorphic* if $f$ and $f^{-1}$ are
holomorphic.

The following two theorems are fundamental in complex analysis.

**Maximum Modulus Principle** [2]
Let $C$ be a simple closed contour in $\mathbb{C}$ and $f : C \mapsto \mathbb{C}$ be
holomorphic, then for $z_0$ in the interior of $C$,

$$|f(z_0)| \leq \max_{z \in C} |f(z)|$$

with equality iff $f$ is constant on $C$.

We can use the maximum modulus to prove the following theorem about
complex functions.

**Schwarz Lemma** [4]
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic with $\varphi(0) = 0$. Then
$|\varphi(z)| \leq |z|$ and $|\varphi'(0)| \leq 1$, with equality iff
$\varphi$ is a rotation.

**Proof**
Let $f(z) = \frac{\varphi(z)}{z}$ for $z \neq 0$ and
$f(0) = \varphi'(0)$. The map $f : \mathbb{D} \mapsto \mathbb{C}$ is holomorphic. Let
$0 < r < 1$ and $|z| \leq r$, by the maximum modulus principle,

$$|f(z)| \leq \max_{|z| \leq r} |f(z)| = \max_{|z| = r} \bigg|\frac{\varphi(z)}{z} \bigg| \leq \max_{|z| = r} \frac{1}{|z|} = \frac{1}{r}$$

Letting $r \to 1$ we obtain $|f(z)| = 1$, in particular
$|\varphi(z)| \leq |z|$ and $|\varphi'(0)| = |f(0)| \leq 1$. If equality
holds for some $z \in \mathbb{D}$, then $|f(z)|$ is constant on $\mathbb{D}$, so
$\varphi(z) = e^{i \theta} z$ for some $\theta \in \mathbb{R}$. If
$\varphi(z) = e^{i \theta} z$ then $|\varphi(z)| = |z|$ and
$\varphi'(z) = e^{i \theta}$ so $|\varphi'(0)| = 1$ and hence the
reverse direction holds.

The following function will be used frequently for its properties of
being an automorphism, mapping a specified point to 0 and being its own
inverse.

**Theorem**
Let $a \in \mathbb{D}$ and $T_a : \bar{\mathbb{D}} \mapsto \mathbb{C}$ defined by,

$$T_a (z) = \frac{a - z}{1 - \bar{a} z}$$

Then $||T_\alpha (z)|| \leq 1$ with equality iff $||z|| = 1$.
$T_a$ is also an automorphism of $\mathbb{D}$.

**Proof**
Let $z \in \partial \mathbb{D}$ and $\alpha \in \mathbb{D}$, then
$||z|| = z \bar{z} = 1$,

$$\begin{aligned}
T_a (z) &= \frac{a - z}{1 - \bar{a} z} & \\
&= \frac{a \bar{z} - 1}{\bar{z} - \bar{a}}  &\bigg( \times \frac{\bar{z}}{\bar{z}} \bigg) \\
&= \frac{(a \bar{z} - 1)(z - a)}{||z - a||^2}  &\bigg( \times \frac{z - \alpha}{z - a} \bigg) \\
&= \frac{(z - a)^2}{z ||z - a||^2}  &\bigg( \times \frac{z}{z} \bigg) \\
||T_a (z) || &= 1 \end{aligned}$$

Since the only pole of $T_a$ is at $1 / \bar{a}$ which is outside the
disk, $T$ is holomorphic and the result follows from maximum modulus
theorem.

$$\begin{aligned}
T_a \circ T_a (z) &= \frac{a - T_a(z)}{1 - \bar{a} T_a (z)} \\
&= \frac{a - \frac{a - z}{1 - \bar{a} z}}{1 - \bar{a}\frac{a - z}{1 - \bar{a} z}} \\
&= \frac{a (1 - \bar{a} z) - (a - z)}{1 - \bar{a} z - \bar{a} (a - z)} \\
&= z\end{aligned}$$

$T_a$ is its own inverse thus $T_a$ is an automorphism of the unit disk.

The Schwarz Lemma is quite restrictive, requiring $f(0) = 0$, so we
extend it to all holomorphic functions. To do this we use the Schwarz
lemma along with the automorphism $T_a$,

**Schwarz Pick Lemma**
Let $\varphi : \mathbb{D} \mapsto \mathbb{D}$ be holomorphic. Then for $u, v \in \mathbb{D}$,

$$|T_{\varphi(u)} (\varphi(v))| \leq |T_{u} (v)|$$


**Proof**
Let $F = T_{\varphi(u)} \circ \varphi \circ T_{u}$. Then,

$$F(0) = T_{\varphi(u)} \circ \varphi \circ T_{u} (0) = T_{\varphi(u)} \circ \varphi (u) = 0$$

Applying the Schwarz Lemma,
$||F(z)|| \leq ||z||$. Let $z = T_u (v)$,
then
$|T_{\varphi(u)} (\varphi(v))| \leq |T_{u} (v)|$

# Hyperbolic Metric

A general metric tensor on the complex plane is given by,

$$ds^2 = \lambda^2 (z, \bar{z}) dz d\bar{z}$$

the length of a curve $\gamma$ in the complex plane is given by,

$$\ell(\gamma) = \int_\gamma ds = \int_\gamma \lambda (z) |dz|$$

and a metric for our space is given by

$$d(u, v) = \inf_\gamma \ell(\gamma)$$

where $\gamma$ is any curve in the space from $u$ to $v$.

We will construct our 'density function' $\lambda$ such that $T_a$ is an
isometry for the metric $d$ on the unit disk $\mathbb{D}$, namely
$d(u, v) = d( T_a(u), T_a(v))$ for any $u, v$.

**Proposition**
The density function $\lambda$ is given by
$$\lambda(z) = \frac{2}{1 - ||z||^2}$$

**Proof**
Let $u, v \in \mathbb{D}$ and $T_a$ an automorphism of the disk. Then,

$$\begin{aligned}
d(u, v) &= \inf_\gamma \int_\gamma \lambda (z) |dz| \\
d(T_a(u), T_a(v)) &= \inf_{\gamma'} \int_{\gamma'} \lambda (z) |dz| \\
&= \inf_\gamma \int_\gamma \lambda (T_a(z)) |T_a'(z)| |dz| \end{aligned}$$

Thus a sufficient condition for $T_a$ to be an isometry is
$\lambda (T_a(z)) |T_a'(z)| = \lambda (z)$.

$$\begin{aligned}
|T_a'(z)| &= \frac{|1 - \bar{a}z + \bar{a} (z - a)|}{|1 - \bar{a} z|^2} \\
&= \frac{1 - |a|^2}{|1 - \bar{a} z|^2} \\
\lambda(T_a(z)) &= \frac{2}{1 - |T_a(z)|^2} \\
&= \frac{2}{1 - |\frac{z - a}{1 - \bar{a} z}|^2} \\
&= \frac{2|1 - \bar{a} z|^2}{|1 - \bar{a}z|^2 - |z - a|^2} \\
&= \frac{2|1 - \bar{a} z|^2}{1 - 2 \Re(\bar{az}) + |\bar{a}z|^2 - ( |z|^2 - 2 \Re(a \bar{z}) + |a|^2)} \\
&= \frac{2|1 - \bar{a} z|^2}{(1 - |a|^2)(1 - |z|^2)} \\
\lambda (T_a(z)) |T_a'(z)| &= \frac{2|1 - \bar{a} z|^2}{(1 - |a|^2)(1 - |z|^2)} \frac{1 - |a|^2}{|1 - \bar{a} z|^2} \\
&= \frac{2}{1 - |z|^2} \\
&= \lambda(z)
\end{aligned}$$

The **Poincaré Disk** is the unit disk in the complex plane along with
the Riemann metric given above. $\mathbb{D}$ refers to the Poincaré disk unless
stated otherwise.

**Example**
We can find an explicit formula for the distance to the origin using the
above integral. Let $u \in \mathbb{D}$, then $\gamma(t) = ut$ for
$0 \leq t \leq 1$

$$\begin{aligned}
d(0, u) &= \int_\gamma \frac{2}{1 - |z|^2} |dz| \\
&= \int_0^1 \frac{2}{1 - |u|^2 t^2} |u| dt \\
&= |u| \int_0^1 \frac{1}{1 + |u|t} + \frac{1}{1 - |u|t} dt \\
&= |u| \bigg( \frac{1}{|u|} \ln(1 + |u|t) - \frac{1}{|u|} \ln(1 - |u|t) \bigg)_0^1 \\
&= \ln(1 + |u|) - \ln(1 - |u|) \\
&= \ln(\frac{1 + |u|}{1 - |u|})
\end{aligned}$$

# Geometry

## Geodesics

Let $u, v \in \mathbb{D}$, the geodesic between $u$ and $v$ is the shortest path
joining them.

**Definition**
Let $u, v \in \mathbb{D}$ and $\gamma$ a curve in $\mathbb{D}$ passing through $u, v$.
$\gamma$ is a geodesic if

$$d(u, v) = \int_\gamma \lambda(z) dz$$

Before we find an explicit formula for a geodesic between two points, we
need some properties of geodesics. Since our density function, $\lambda$
only depends on $|z|$, the geodesic between the origin and another point
is a straight line.

Let $u, v$ lie on the interior of $\mathbb{D}$. The automorphism
$\varphi(z) = \frac{z - u}{1 - \bar{u} z}$ maps $u \mapsto 0$. As
$\varphi$ is an isometry for the unit disk, it maps the geodesic between
$u$ and $v$ goes to the straight line between $0$ and $\varphi(v)$. Thus
if we extend the geodesic towards the boundary, the straight line
intersects the boundary at right angles, and since the automorphisms are
conformal maps [@conformal], the geodesic between $u$ and $v$ intersects
the boundary at right angles. Moreover Möbius transformations take
circles to circles, and a straight line can be considered as a circle
through infinity on the Riemann sphere, thus the geodesic between $u$
and $v$ is an arc of a circle. To find the geodesics we make use of the
following proposition,

**Proposition**
In the Euclidean plane $\mathbb{R}^2$, the circle $x^2 + y^2 + ax + by + 1 = 0$
intersects the circle $x^2 + y^2 = 1$ at right angles.

**Proof**
Let $C_1$ denote the circle $x^2 + y^2 + ax + by + 1 = 0$ and $C_2$
denote $x^2 + y^2 = 1$. Substituting $C_2$ into $C_1$,
$$ax + by + 2 = 0$$

Differentiating $C_1$ w.r.t $x$, $$2x + a + (2y + b) y' = 0$$

Thus a tangent vector is given by
$$(1, y') = \bigg( 1, - \frac{2x + a}{2y + b} \bigg)$$

Similarly for $C_1$,
$$2x + 2y y' = 0 \Rightarrow (1, y') = \bigg(1, \frac{x}{y} \bigg)$$

Thus,

$$\begin{aligned}
C'_1 \cdot C'_2 &= \bigg( 1, - \frac{2x + a}{2y + b} \bigg) \cdot \bigg(1, \frac{x}{y} \bigg) \\
&= 1 + \frac{2x + a}{2y + b} \bigg(1, \frac{x}{y} \bigg) \\
&= \frac{ y (2y + b) + x (2x + a) }{ (2y + b) y } \\
&= \frac{ 2 + ax + by }{ (2y + b) y } \\
\text{Since } ax + by + 2 &= 0 \text{ at the intersection of $ C_1 $ and $ C_2 $,} \\
C'_1 \cdot C'_2 &= 0\end{aligned}$$

Therefore $C_1$ intersects $C_2$ at right angles.

**Example**
Let $v = v_0 + i v_1, w = w_0 + i w_1 \in \partial \mathbb{D}$. The
geodesic passing through $v$ and $w$ is given by
$x^2 + y^2 + ax + by + 1 = 0$ for appropriate $a$ and $b$. Substituting
$v$ and $w$,

$$\begin{aligned}
0 &= v_0^2 + v_1^2 + a v_0 + b v_1 + 1 \\
0 &= w_0^2 + w_1^2 + a w_0 + b w_1 + 1 \\
\begin{pmatrix} v_0 & v_1 \\ w_0 & w_1 \end{pmatrix} \begin{pmatrix} a \\ b \end{pmatrix} &= \begin{pmatrix} -1 - v_0^2 - v_1^2 \\ -1 - w_0^2 - w_1^2 \end{pmatrix} \\
\begin{pmatrix} a \\ b \end{pmatrix} &= \frac{-1}{v_0w_1 - v_1w_0} \begin{pmatrix} w_1 & -v_1 \\ -w_0 & v_0 \end{pmatrix} \begin{pmatrix} 1 + |v|^2 \\ 1 + |w|^2 \end{pmatrix} \\
\text{Therefore,} \\
a &= \frac{v_1 (1 + |w|^2) - w_1 (1 + |v|^2)}{ v_0w_1 - v_1w_0 } \\
b &= \frac{w_0 (1 + |v|^2) - v_0 (1 + |w|^2)}{ v_0w_1 - v_1w_0 }
\end{aligned}$$

Substituting these into the formula for the circle,
$x^2 + y^2 + ax + by + 1 = 0$, we obtain an explicit expression for the
geodesic between $v$ and $w$

## Triangles

Now we find a formula for the area of a triangle in the disk. Using the
results from the previous section, the Riemann metric for the unit disk
is given by

$$ds^2 = \frac{4}{(1 - |z|^2)^2} |dz|^2$$

Writing $dz = dx + dy i$, we find the first fundamental form
for $ds^2$
$\big( ds^2 = E dx^2 + 2F dx dy + G dy^2 \big)$ has
coefficients,

$$\begin{aligned}
E &= \frac{4}{(1 - |z|^2)^2} \\
F &= 0 \\
G &= \frac{4}{(1 - |z|^2)^2}\end{aligned}$$

Thus we can compute the curvature of $\mathbb{D}$ using the following
formula [6]

**Theorem**
For a parametrisation with $F = 0$, the Gaussian curvature $K$ is given
by,

$$K = \frac{-1}{2 \sqrt{EG}} \bigg( \frac{\partial}{\partial x} \frac{G_x}{\sqrt{EG}} + \frac{\partial}{\partial y} \frac{E_y}{\sqrt{EG}} \bigg)$$

**Example**
Calculating $K$ for the Poincaré disk.

$$\sqrt{EG} = E$$

$$\begin{aligned}
G_x &= \partial_x \frac{4}{1 - x^2 - y^2} & E_y &= \partial_y \frac{4}{1 - x^2 - y^2} \\
&= \frac{16 x}{(1 - x^2 - y^2)^3} &&= \frac{16y}{(1 - x^2 - y^2)^3}   \\
\partial_x \frac{G_x}{\sqrt{EG}} &= \partial_x \frac{16 x}{1 - x^2 - y^2} & \partial_y \frac{E_y}{\sqrt{EG}} &= \partial_y \frac{16y}{1 - x^2 - y^2} \\
&= \frac{4(1 - x^2 - y^2) + 8x^2}{(1 - x^2 - y^2)^2} &&= \frac{4(1 - x^2 - y^2) + 86^2}{(1 - x^2 - y^2)^2} \\
&= \frac{4(1 + x^2 - y^2)}{(1 - x^2 - y^2)^2} &&= \frac{4(1 - x^2 + y^2)}{(1 - x^2 - y^2)^2}\end{aligned}$$

$$\begin{aligned}
K &= \frac{-1}{2 \sqrt{EG}} \bigg( \partial_x \frac{G_x}{\sqrt{EG}} + \partial_y \frac{E_y}{\sqrt{EG}} \bigg) \\
&= \frac{- (1 - x^2 - y^2)^2}{8} \bigg( \frac{4(1 + x^2 - y^2)}{(1 - x^2 - y^2)^2} + \frac{4(1 - x^2 + y^2)}{(1 - x^2 - y^2)^2} \bigg) \\
&= \frac{- (1 - x^2 - y^2)^2}{8} \frac{8}{(1 - x^2 - y^2)^2} \\
&= -1\end{aligned}$$

Therefore $\mathbb{D}$ has Gaussian curvature $-1$. The Poincaré Disk is
referred to as a model for the hyperbolic plane since they both have
constant negative curvature.

For a general triangle in the Poincaré disk, we can calculate its area
using Gauss-Bonnet [5]

**Gauss-Bonnet Theorem**
Suppose $M$ is a compact two dimensional Riemannian manifold with
boundary $\partial M$. Let $K$ be the Gaussian curvature of $M$ and
$k_g$ be the geodesic curvature of $\partial M$. Then,

$$\int_M K dA + \int_{\partial M} k_g ds = 2 \pi \chi(M)$$

where $dA$ is the area element, $ds$ is the line element and
$\chi(M)$ is the Euler characteristic of $M$. Reformulated for a
geodesic triangle $T$ (the sides of the triangle lie of geodesics),

$$\int_T K = \alpha + \beta + \gamma - \pi$$

where $\alpha, \beta, \gamma$ are the interior angles of $T$.

**Example**
We found previously that $K = -1$, therefore

$$\int_T =  A = \pi - (\alpha + \beta + \gamma)$$

For right angled triangles we have a nice relationship between the side
lengths not dissimilar from the Pythagorean Theorem for Euclidean right
angled triangles.

**Theorem**
Let $\triangle(ABC)$ be a right angled triangle in $\mathbb{D}$ with one vertex
at the origin, side lengths $a$, $b$ and hypotenuse $c$. Then,

$$\cosh a \cosh b = \cosh c$$

**Proof**
Without loss of generality, we assume $B = u$ lies on the $\Re$ axis and
$C = vi$ on the $\Im$ axis, since rotations are isometries of the unit
disk.

![Triangle](/assets/report/triangle.JPG)

The geodesic from $0$ to $u$ is the straight line lying on the real
axis, thus the integral in $d_\mathbb{D}$ becomes a standard single variable
integral,

$$\begin{aligned}
a &= \int_0^u \frac{2}{1 - t^2} dt \\
&= \int_0^u \frac{1}{1 + t} + \frac{1}{1 - t} dt \\
&= \ln(1 + t) - \ln(1 - t) \big|_{t = 0}^u \\
&= \ln(\frac{1 + u}{1 - u}) \\
\text{Similarly for $ v $} \\
b &= \ln(\frac{1 + v}{1 - v})
\end{aligned}$$

Since the line $BC$ doesn't lie on a straight line through the origin,
we can't use the same procedure. Instead take the automorphism of the
unit disk,

$$\varphi(z) = \frac{z - vi}{1 + viz}$$

This maps $v \mapsto 0$ and $u \mapsto \frac{u - vi}{1 + uiv}$. Then we
take the integral over $\gamma(t) = \varphi(u) t$ for $t \in [0, 1]$.

$$\begin{aligned}
c &= \int_0^1 \frac{2|\varphi(u)|}{1 - |\varphi(u)|^2 t^2} dt \\
&= | \varphi(u) | \int_0^1 \frac{1}{1 + |\varphi(u) t} + \frac{1}{1 - | \varphi(u) t} dt \\
&= \ln(\frac{ 1 + |\varphi(u)| }{ 1 - |\varphi(u)|})
\end{aligned}$$

Now we build up to the LHS of the equality,

$$\begin{aligned}
\cosh x &= \frac{e^x + e^{-x}}{2} \\
\cosh \ln x &= \frac{e^{\ln x} + e^{-\ln x}}{2} \\
&= \frac{x + \frac{1}{x}}{2} \\
\cos \ln \frac{1 + u}{1 - u} &= \frac{\frac{1 + u}{1 - u} + \frac{1 - u}{1 + u}}{2} \\
&= \frac{(1 + u)^2 + (1 - u)^2}{2 (1 - u)^2} \\
&= \frac{1 + u^2}{1 - u^2}
\end{aligned}$$

Therefore,

$$\cosh a \cosh b = \frac{1 + u^2}{1 - u^2} \frac{1 + v^2}{1 - v^2}$$

Switching our attention to the RHS,

$$\begin{aligned}
\cosh c &= \frac{1 + |\varphi(u)|^2}{1 - |\varphi(u)|^2} \\
&= \frac{1 + \big| \frac{ u - vi }{ 1 + uiv } \big|^2 }{ 1 - \big| \frac{ u - vi }{ 1 + uiv } \big|^2} \\
&= \frac{ |1 + uvi|^2 + |u - vi|^2 }{ |1 + uvi|^2 - |u - vi|^2 } \\
&= \frac{1 + u^2 v^2 + u^2 + v^2}{1 + u^2v^2 - u^2 - v^2} \\
&= \frac{(1 + u^2)(1 + v^2)}{(1 - u^2)(1 - v^2)}
\end{aligned}$$

Therefore,

$$\cosh a \cosh b = \cosh c$$
