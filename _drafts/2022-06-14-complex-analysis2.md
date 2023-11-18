---
title: Upper Half Plane (2/6)
date: 2022-06-14 11:00
categories: [Complex Analysis, Holomorphic Dynamics and Möbius Transformations]
tags: [möbius transformations, algebraic semigroups]     # TAG names should always be lowercase
math: true
comments: false
---

[//]: <> (Convert Latex to Markdown, Add newlines to seperate equations)
[//]: <> (pandoc EulerIdentity.tex -o test1.md --mathml)

# Hyperbolic Metric

Similarly to the Poincaré Disk, we will find the Riemann metric for the
upper half plane $\mathbb{H} = \\{ z \in \mathbb{C}  |  \Im(z) > 0 \\\}$. To avoid confusion
we will denote the density and Riemann metric on $\mathbb{D}$ as $\lambda_{\mathbb{D}}$
and $d_{\mathbb{D}}$ respectively and the corresponding functions on the upper
half plane as $\lambda_{\mathbb{H}}$ and $d_{\mathbb{H}}$.

**Proposition**
The density function $\lambda_{\mathbb{H}}$ for the upper half plane
preserving the metric in Poincaré disk is given by,

$$\lambda_{\mathbb{H}}(z) = \frac{1}{\Im(z)}$$

**Proof**
Let $\varphi: \mathbb{D} \mapsto \mathbb{H}$ be defined by
$\varphi(z) = \frac{z + i}{1 + iz}$. Then similarly to the Poincaré
disk, we can use change of variables to move from $\mathbb{H}$ to $\mathbb{D}$,

$$\begin{aligned}
\lambda_{\mathbb{D}}  ( \varphi(z)) &= \frac{1}{1 - |\varphi(z)|^2} \\
&= \frac{1 |1 + iz|^2}{|1 + iz|^2 - |z + i|^2} \\
&= \frac{|1 + iz|^2}{2\Im(z)} \\
|\varphi'(z)| &= \frac{2}{|1 + iz|^2} \\
\lambda_{\mathbb{H}}(z) &= | \varphi'(z) | \lambda_{\mathbb{D}} (\varphi(z)) \\
&= \frac{2}{|1 + iz|^2} \frac{|1 + iz|^2}{2\Im(z)} \\
&= \frac{1}{\Im(z)}
\end{aligned}$$

When we studied the Poincaré disk, we started with automorphisms of the
unit disk, and found a Riemann metric with those automorphisms as the
isometries for the metric. Now we have a Riemann metric on the upper
half plane, and we want to find the automorphisms of $\mathbb{H}$ which
are isometries for $d_{\mathbb{H}}$.

**Definition**
Let $a, b, c, d \in \mathbb{C}$ satisfying $ad - bc \neq 0$ then

$$A(z) = \frac{az + b}{cz + d}$$

is a Möbius transformation.

We can identify the coefficients $a, b, c, d$ with the entries of a 2x2
matrix, namely

$$\begin{pmatrix}  a & b \\ c & d \end{pmatrix} \to \frac{az + d}{cz + d}$$

Suppose we have a Möbius Transformation $\varphi$ with coefficients
$a, b, c, d \in \mathbb{R}$.

**Proposition**
The map $f$ defined by identifying the matrix entries with a Möbius
transformation is a homomorphism from SL$(2, \mathbb{R})$ to the group of Möbius
transformations under composition.

**Proof**
We need to check that $f(xy) = f(x) f(y)$, or equivalently $f(xy)(z) = f(x) \circ f(y) (z)$ for all $z \in \mathbb{C}$. Let

$$x = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \qquad
y = \begin{pmatrix} e & f \\ g & h \end{pmatrix} \in \text{SL}(2, \mathbb{R})$$

Then,

$$\begin{aligned}
f(xy)(z) &= f \bigg( \begin{pmatrix} a & b \\ c & d \end{pmatrix} \begin{pmatrix} e & f \\ g & h \end{pmatrix} \bigg) (z) \\
&= f \begin{pmatrix} ae + bg & af + bh \\ ce + dg & cf + dh \end{pmatrix} (z) \\
&= \frac{(ae + bg) z + af + bh}{(ce + dg) z + cf + dh} \\
f(x) \circ f(y) (z) &= f \begin{pmatrix} a & b \\ c & d \end{pmatrix} \circ f \begin{pmatrix} e & f \\ g & h \end{pmatrix} (z) \\
&= f \begin{pmatrix} a & b \\ c & d \end{pmatrix} \bigg( \frac{ ez + f }{ gz + h } \bigg) \\
&= \frac{ a \frac{ ez + f }{ gz + h } + b }{ c \frac{ ez + f }{ gz + h } + d } \\
&= \frac{ a (ez + f) + b (gz + h)}{ c (ez + f) + d (gz + h)} \\
&= f(xy) (z)\end{aligned}$$

This homomorphism is surjective with kernel consisting of $\\{ I, -I \\}$.
Thus we call the quotient SL$(2, \mathbb{R}) / \\{ I, -I \\}$ the projective
special linear group, PSL$(2, \mathbb{R})$ which is isomorphic to the group of
Möbius transformations.

From this point onwards, it is assumed that a Möbius transformation
$\varphi$ has real coefficients $a, b, c, d \in \mathbb{R}$ such that
$ad - bc = 1$ unless stated otherwise.

**Proposition**
The Möbius transformations are automorphisms of $\mathbb{H}$ and
isometries for $d_{\mathbb{H}}$.

**Proof**
$\varphi$ maps the real axis to itself, so it suffices to check that a
point on the interior of $\mathbb{H}$ is mapped back into the interior
of $\mathbb{H}$.

$$\begin{aligned}
\varphi(i) &= \frac{ai + b}{ci + d} \\
&= \frac{bd + ac + i}{c^2 + d^2}
\end{aligned}$$

Therefore $\varphi(i)$ is in the interior of $\mathbb{H}$ and $\varphi$
is an automorphism of $\mathbb{H}$. To show $\varphi$ is an isometry for
$\mathbb{H}$, we have the same sufficient condition as the unit disk,

$$\lambda_{\mathbb{H}}(z) = | \varphi'(z) | \lambda_{\mathbb{H}} (\varphi(z))$$

for any $z \in \mathbb{H}$ then $\varphi$ is an isometry. Let
$z = x + iy \in \mathbb{C}$

$$\begin{aligned}
\varphi(z) &= \frac{a(x + iy) + b}{c(x + iy) + d} \\
&= \frac{(ax + b + i ay) (cx + d - icy)}{(cx + d)^2 + y^2} \\
\Im(\varphi(z)) &= \frac{ay ( cx + d ) - cy ( ax + b )}{|cz + d|^2} \\
&= \frac{xy (ac - ac) + y (ad - bc)}{|cz + d|^2} \\
&= \frac{\Im(z)}{|cz + d|^2} \\
|\varphi'(z)| &= \frac{a(cz + d) - c(az + b)}{|cz + d|^2} \\
&= \frac{1}{|cz + d|^2} \\
| \varphi'(z) | \lambda_{\mathbb{H}} (\varphi(z)) &= | \varphi'(z) | \frac{1}{\Im(\varphi(z))} \\
&= \frac{1}{|cz + d|^2} \frac{|cz + d|^2}{\Im(z)} \\
&= \lambda_{\mathbb{H}} (z)
\end{aligned}$$

Therefore $\varphi$ is an isometry of $\mathbb{H}$.

Möbius Transformations will be studied in more detail in the next
chapter.

# Geometry

## Geodesics

As with the Poincaré Disk, we will describe the geodesics and triangles
of the upper half plane. Let $u, v \in \mathbb{D}$, the geodesic between $u$ and
$v$ is the shortest path joining them.

**Definition**
Let $u, v \in \mathbb{D}$ and $\gamma$ a curve in $\mathbb{H}$ passing through
$u, v$. $\gamma$ is a geodesic if

$$d_\mathbb{H}(u, v) = \int_\gamma \lambda_\mathbb{H}(z) dz$$

The discussion in the poincare disk geometry section applies here, we want
circles that intersect the real axis at right angles.

**Proposition**
In the Euclidean plane $\mathbb{R}^2$, the circle $(x - a)^2 + y^2 = r^2$
intersects the x axis at right angles.

Thus to find the geodesic we solve the linear system with
$u = u_0 + u_1 i$ and $v = v_0 + v_1 i$ lying on that line for $a, r$,

$$\begin{aligned}
a &= \frac{|u|^2 - |v|^2}{2 (u_0 + v_0)} \\
r^2 &= (u_0 - a)^2 + u_1^2
\end{aligned}$$

## Triangles

Following the same methodology as in poincare disk triangles section, we find the upper half
plane has constant negative curvature $-1$. Thus $A = \pi - (\alpha + \beta + \gamma)$
