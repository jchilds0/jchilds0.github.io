---
title: Algebraic Semigroups (5/6)
date: 2022-06-14 14:00
categories: [Complex Analysis, Holomorphic Dynamics and Möbius Transformations]
tags: [möbius transformations, algebraic semigroups]     # TAG names should always be lowercase
math: true
comments: false
---

[//]: <> (Convert Latex to Markdown, Add newlines to seperate equations)
[//]: <> (pandoc EulerIdentity.tex -o test1.md --mathml)

# Preliminaries

Before we can study semigroups, we need some definitions from topology
and algebra

## Topology

**Definition**
A *topology* of a set $X$ is a collection $U$ of subsets of $X$ called
*open sets* such that,

1.  An arbitrary union of elements of $U$ is an element of $U$

2.  A finite intersection of elements of $U$ is an element of $U$

3.  $X$ and $\emptyset$ are elements of $U$

A special type of subset of a topological space is a compact set,

**Definition**
Let $X$ be a topological space. A set $K \subset X$ is *compact* if any
open cover has a finite sub cover. More explicitly for any collection
$C = \{ U_1, U_2, ... \}$ of open sets in $X$ such that

$$K \subset \bigcup_{U \in C} U$$

there exists a finite subset of $C$, $\{ U_1, ..., U_k \}$ such that

$$K \subset \bigcup_{i = 1}^k U_i$$

Two properties of topological spaces are as follows,

**Definition**
Let $X$ be a topological space. $X$ is *Hausdorff* if for any two points
$x, y \in X$ such that $x \neq y$, there exists open sets $U_x , U_y$
containing $x, y$ respectively such that $U_x \cap U_y = \emptyset$.

The definition for a topology above is stronger than required, so we
reduced collection of open sets known as a basis,

**Definition**
A *base* for a topology on $X$ is a collection of open sets $U'$ such
that,

1.  A finite intersection of elements of $U'$ is an element of $U'$

2.  $X$ and $\emptyset$ are elements of $U'$

We can construct a topology from a base by taking arbitrary unions of
elements of $U'$. The final property of topological spaces we are
interested in is the size of a basis for a topological space,

**Definition**
Let $X$ be a topological space. $X$ is *second countable* if $X$ has a
countable base.

We can reduce the size of our collection of open sets further to a
subbase,

**Definition**
A *subbase* for a topology on $X$ is a collection of open sets $U''$
such that,

1.  $X$ and $\emptyset$ are elements of $U''$

We can construct a base from a subbase by taking finite intersections of
elements of $U''$. A subbase allows us to abstract away the axioms for a
topology, greatly simplifying the construction and verification of
topologies.

**Definition**
Let $X, Y$ be topological spaces and $C(X, Y)$ be the collection of all
continuous maps from $X$ to $Y$. Given a compact set $K \subset X$ and
an open set $U \subset Y$, let $V(K, U)$ denote the set
$\{ f \in C(X, Y) \ | \ f(K) \subset U \}$. The collection $V(K, U)$ is
a subbase for the *compact-open topology* on $C(X, Y)$

This is clearly a subbase as $V(K, \emptyset) = \emptyset$ and
$V(\emptyset, Y) = C(X, Y)$.

## Algebra

**Definition**
A *semigroup* is a set $X$ with an associative binary operation
$*: X \times X \mapsto X$. Namely, for any $x, y, z \in X$,

$$(x * y) * z = x * (y * z)$$

While semigroups will lead to interesting results in the following
sections, we will also want an object with more structure that we can
completely characterise.

**Definition**
A *group* is a set $X$ with a binary operation
$* : X \times X \mapsto X$ such that,

1.  (Identity) $e \in X$ such that $x * e = e * x = x$ for all
    $x \in X$.

2.  (Inverse) For all $x \in X$ there exists $y \in X$ such that
    $x * y = y * x = e$.

3.  (Associativity) For all $x, y, z \in X$,
    $x * (y * z) = (x * y) * z$.

The most general way of mapping between two (semi) groups is as follows,

**Definition**
Let $(G_0, *_0)$ and $(G_1, *_1)$ be a (semi)group. A map
$f : G_0 \mapsto G_1$ is a *homomorphism* if for any $x, y \in G_0$,

$$f(x *_0 y) = f(x) *_1 f(y)$$

A stronger map is an isomorphism, which basically says the two objects
have the same group structure.

**Definition**
Let $f$ be a homomorphism. Then $f$ is an *isomorphism* if $f$ is
bijective (injective and surjective).

A special type of isomorphism is one from an object to itself,

**Definition**
Let $f$ be an isomorphism. Then $f$ is an *automorphism* if $G_0 = G_1$
from the definition of a homeomorphism.

# Semigroups in the Unit Disk

In the previous chapter we iterated Möbius transformations by repeatedly
composing them. This is essentially a map
$\mathbb{N} \ni n \mapsto \varphi^{\circ n}$. Now we extended this idea
to real numbers and general holomorphic self-maps of the unit disc. This
chapter follows Chapter 8 of [4].

**Definition**
An *algebraic semigroup $(\varphi_t)$* of holomorphic self maps of the
unit disk is a homomorphism between the additive semigroup of non
negative real numbers and the composition semigroup of all holomorphic
self maps of the unit disk. Namely,

1.  $\varphi_t \in \text{Hol} ( \mathbb{D}, \mathbb{D} )$ for all $t \geq 0$

2.  $\varphi_0 = \text{id}_\mathbb{D}$

3.  $\varphi_{s + t} = \varphi_{s} \circ \varphi_t$ for all
    $s, t \geq 0$

**Definition**
An algebraic semigroup $(\varphi_t)$ is continuous if the map

$$[0, \infty) \ni t \mapsto \varphi_t \in \text{Hol}(\mathbb{D}, \mathbb{D})$$

where $[0, \infty)$ has the usual topology and $Hol(\mathbb{D}, \mathbb{D})$ has the
compact-open topology.

Both of these definitions translate directly to Riemann surfaces.

**Proposition**
Let $h$ be a biholomorphism from $\mathbb{D}$ onto a domain $\Omega$ of the
complex plane. If $(\phi_t)$, $t \geq 0$ is a family of holomorphic self
maps of $\Omega$ such that,

1.  $\varphi_0 = id_\Omega$

2.  $\varphi_{s + t} = \varphi_s \circ \varphi_t$

3.  $[0, \infty) \ni t \mapsto \varphi_t \in \text{Hol}(\Omega, \Omega)$
    is continuous where $[0, \infty)$ has the unsual topology and
    $\text{Hol}(\Omega, \Omega)$ has the compact-open topology

Then $\varphi_t^h = h^{-1} \circ \varphi_t \circ h$ is a continuous
semigroup in $\mathbb{D}$.

**Proof**
The proof is a direct verification of the semigroup conditions,

1. $\varphi_t$ is the composition holomorphic functions

2. $t = 0$ is the identity

    $$\begin{aligned}
    \varphi_0^h &= h^{-1} \circ \varphi_0 \circ h \\
    &= h^{-1} \circ id_\Omega \circ h \\
    &= h^{-1} \circ h \\
    &= id_\mathbb{D}
    \end{aligned}$$

3. Homomorphism condition

    $$\begin{aligned}
    \varphi_{t + s}^h &= h^{-1} \circ \varphi_{t + s} \circ h \\
    &= h^{-1} \circ \varphi_t \circ \varphi_s \circ h \\
    &= h^{-1} \circ \varphi_t \circ h \circ h^{-1} \circ \varphi_s \circ h \\
    &= \varphi_t^h \circ \varphi_s^h
    \end{aligned}$$

Holomorphic maps are continuous and the composition of continuous maps
is continuous, thus $\varphi_t^h$ is continuous.

# Groups in the Unit Disk

**Definition**
An *algebraic group* $(\varphi_t)$ of holomorphic self maps of the unit
disk is an algebraic semigroup in $\mathbb{D}$ such that
$\varphi_t \in \text{Aut} (\mathbb{D}, \mathbb{D})$ for all $t \geq 0$.

Then we define $\varphi_{-t} = (\varphi_t)^{-1}$

The condition of all iterates being automorphisms is a stronger
condition than necessary. We can give an equivalent condition as
follows.

**Theorem**
Let $(\varphi_t)$ be a semigroup in $\mathbb{D}$. $(\varphi_t)$ is a group in
$\mathbb{D}$ iff there exists $t > 0$ such that
$\varphi_t \in \text{Aut}(\mathbb{D}, \mathbb{D})$.

**Proof**
The forward direction follows from the definition of an algebraic group.

$( \Leftarrow )$ Let $(\varphi_t)$ be a semigroup in $\mathbb{D}$ such that
$\varphi_{t_0} \in \text{Aut}(\mathbb{D}, \mathbb{D})$. Let $0 < s < t_0$, then

1. Surjective
    $$\mathbb{D} = \varphi_{t_0} (\mathbb{D}) = \varphi_s ( \varphi_{t_0 - s} (\mathbb{D})) \subset \varphi_s (\mathbb{D})$$

2. Injective. Let $u, v \in \mathbb{D}$ be distinct. Since $\varphi_{t_0} \in \text{Aut} (\mathbb{D}, \mathbb{D})$,
    $\varphi_{t_0} (u) \neq \varphi_{t_0} (v)$. Suppose $\varphi_s (u) = \varphi_s (v)$,

    $$\begin{aligned}
    \varphi_{t_0} (u) &= \varphi_{t_0 - s} (\varphi_s (u)) \\
    &= \varphi_{t_0 - s} (\varphi_s (v)) \\
    &= \varphi_{t_0} (v)
    \end{aligned}$$

    Which contradicts $\varphi_{t_0}$ is injective. Thus $\varphi_s$ is injective

If $s > t_0$ then $s = n t_0 + r$ for some integer $n$ and
$0 < r < t_0$, thus the same results apply to $\varphi_s$ and therefore
$(\varphi_t)$ is an algebraic group.

Since an element of an algebraic group in an automorphism, we can
classify each iterate by their fixed points. We won't prove it here, but
a fixed point of one iterate is a common fixed point of all iterates,
thus we have the following classification.

**Theorem**
Let $( \varphi_t )$ be a non trivial group in $\mathbb{D}$. Then $(\varphi_t)$
has one of the three following forms,

1.  **(Elliptic)** There exists $\tau \in \mathbb{D}$ (Denjoy-Wolff point) and
    $\omega \in \mathbb{R} - \{ 0 \}$ such that,

    $$\varphi_t (z) = \frac{(e^{-i \omega t} - |\tau|^2) z + \tau (1 - e^{-i \omega t})}{\bar{\tau} (e^{-i \omega t} - 1) z + 1 - |\tau|^2 e^{-i \omega t}}$$

2.  **(Parabolic)** There exists $\tau \in \partial \mathbb{D}$ (Denjoy-Wolff
    point) and $\alpha \in \mathbb{R} - \{ 0 \}$ such that,

    $$\varphi_t (z) = \frac{(1 - i \alpha t) z + i \alpha t \tau}{-i \alpha \bar{\tau} t z + 1 + i \alpha t}$$

3.  **(Hyperbolic)** There exists $\tau, \sigma \in \partial \mathbb{D}$ with
    $\tau$ being the Denjoy-Wolff point, $\sigma$ the other fixed point
    and $\alpha \in \mathbb{R} - \{ 0 \}$ such that,

    $$\varphi_t (z) = \frac{(\sigma - \tau e^{\alpha t}) z + \tau \sigma (e^{\alpha t} - 1)}{(1 - e^{\alpha t}) z + \sigma e^{\alpha t} - \tau}$$

**Example**
Let $\tau = 1$ and $\alpha = 1$. Iterating $\varphi_t$, on the
upper half plane the points are translated along horoballs at the fixed
point, moving away from one side of the fixed point towards the other.

<iframe width=720 height=400 src="/assets/report/types/Parabolic%20-%20Tau%20-%201,%20Alpha%20-%201.mp4" frameborder="0" allowfullscreen></iframe>

Let $\tau = i$ and $\alpha = 1$. Iterating $\varphi_t$, on the upper
half plane the points are translated along horoballs at the fixed point.
Since the fixed point is at $\infty$, the horoballs are horizontal
lines, so the points are simply translated in the plane.

<iframe width=720 height=400 src="/assets/report/types/Parabolic%20-%20Tau%20-%20i,%20Alpha%20-%201.mp4" frameborder="0" allowfullscreen></iframe>

**Example**
Let $\tau = 0.5$ and $\omega = \frac{\pi}{2}$. Iterating $\varphi_t$,
the points orbit around the fixed point, $0.5$.

<iframe width=720 height=400 src="/assets/report/types/Elliptic%20-%20Tau%20-%200.5,%20Omega%20-%20pi%20%200.5.mp4" frameborder="0" allowfullscreen></iframe>

**Example**
Let $\sigma = 1$, $\tau = i$ and $\alpha = 1$. Iterating $\varphi_t$,
the points move away from one fixed points towards the other along
geodesics, similarly to the behaviour of Hyperbolic Möbius
transformations

<iframe width=720 height=400 src="/assets/report/types/Hyperbolic%20-%20Sigma%20-%200,%20Tau%20-%20i,%20Alpha%20-%201.mp4" frameborder="0" allowfullscreen></iframe>

Let $\sigma = 1$, $\tau = -1$ and $\alpha = 1$.

<iframe width=720 height=400 src="/assets/report/types/Hyperbolic%20-%20Sigma%20-%201,%20Tau%20-%20-1,%20Alpha%20-%201.mp4" frameborder="0" allowfullscreen></iframe>

# On other Riemann Surfaces

**Definition**
A connected, Hausdorff, second countable topological space $S$ is a
*Riemann Surface* if the exists an open covering $\{ U_\alpha \}$ of
$S$, continuous maps $\psi_\alpha : U_\alpha \mapsto \mathbb{C}$ such that
$\psi_\alpha (U_\alpha)$ is an open subset of $\mathbb{C}$ and
$\psi_\alpha : U_\alpha \mapsto \psi_\alpha(U_\alpha)$ is a
homeomorphism and such that for every $\alpha, \beta$ with
$U_\alpha \cap U_\beta \neq \emptyset$ the map,

$$\psi_\alpha \circ \psi_\beta^{-1} : \psi_\beta(U_\alpha \cap U_\beta) \mapsto \psi_\alpha(U_\alpha \cap U_\beta)$$
is holomorphic.

The family $\{ U_\alpha, \psi_\alpha \}$ is called a *holomorphic atlas*
for $S$ and $\psi_\alpha$ is a *holomorphic chart* of $S$ on $U_\alpha$.
We defined holomorphic maps using the Cauchy Riemann Equations, and we
now extend the notion of holomorphic to general maps of surfaces,

**Definition**
A continuous map $f : S_1 \mapsto S_2$ between two Riemann surfaces
$S_1, S_2$ is *holomorphic* if for every $p \in S_1$ there exists a
holomorphic chart $(U, \psi)$ of $S_1$ with $p \in U$ and a holomorphic
chart $(V, \eta)$ of $S_2$ with $f(p) \in V$ such that the function

$$\eta \circ f \circ \psi^{-1} : \psi(U \cap f^{-1} (V)) \mapsto \eta(V)$$
is holomorphic.

Before we discuss semi groups in the unit disk in detail, we briefly
discuss other Riemann surfaces to justify this investigation. The
following theorem allows us to reduce the space of Riemann surfaces down
to 3 surfaces unique up to biholomorphism.

**Theorem**
Every simply connected Riemann surface is biholomorphic to either the
unit disk $\mathbb{D}$, or the complex plane $\mathbb{C}$, or the Riemann sphere
$\mathbb{C}_\infty$.

We can give a complete classification of semi groups in $\mathbb{C}$ and
$\mathbb{C}_\infty$.

**Theorem**
Let $(\varphi_t)$ be a non trivial continuous semigroup in $\mathbb{C}$. Then
there exists an affine transformation $T$ in $\mathbb{C}$ such that either,

1.  $T \circ \varphi_t \circ T^{-1} (z) = z + it$, or

2.  $T \circ \varphi_t \circ T^{-1} (z) = e^{at} z$, for some non zero
    $a \in \mathbb{C}$

In particular, every continuous semigroup in $\mathbb{C}$ is a continuous group.

**Theorem**
Let $(\varphi_t)$ be a non trivial semigroup in $\mathbb{C}_\infty$. Then there
exists a Mobius transformation $T$ such that either,

1.  $T \circ \varphi_t \circ T^{-1} (z) = z + it$, or

2.  $T \circ \varphi_t \circ T^{-1} (z) = e^{at} z$, for some non zero
    $a \in \mathbb{C}$

In particular, every continuous semigroup in $\mathbb{C}_\infty$ is a continuous
group.

Thus the unit disk is the most interesting domain in which to study semi
groups, in particular semi groups which are not groups since we have a
complete classification of groups in the unit disk.
