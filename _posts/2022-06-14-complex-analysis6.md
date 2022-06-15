---
title: Holomorphic Models (6/6)
date: 2022-06-14 15:00
categories: [Complex Analysis, Holomorphic Dynamics and Möbius Transformations]
tags: [möbius transformations, algebraic semigroups]     # TAG names should always be lowercase
math: true
comments: false
---

[//]: <> (Convert Latex to Markdown, Add newlines to seperate equations)
[//]: <> (pandoc EulerIdentity.tex -o test1.md --mathml)

# Holomorphic Models

This chapter follows Chapter 9 of [4]. The idea behind models
is to model the dynamic behaviour of a semigroup in $\mathbb{D}$ using a group
on a Riemann surface. A candidate for models is the property of semi
conjugation,

**Definition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $\Omega$ be a Riemann Surface
and $(\psi_t)$ a semigroup in $\Omega$. $(\phi_t)$ is semi conjugated to
$(\psi_t)$ if there exists a holomorphic map $g: \mathbb{D} \mapsto \Omega$ such
that for all $t \geq 0$,

![Semiconjugation](/assets/report/tikzcd-1.JPG)

is a commutative diagram.

To motivate the definition of a model, lets investigate semi conjugation
for two similar semi groups. Let $\psi_t (z) = z + it$, $(\psi_t)$ is a
group of automorphisms of $\mathbb{C}$. Let
$C_1 : \mathbb{D} \mapsto H = \{ z \in \mathbb{C} \ | \ \Re(z) > 0 \}$ be the
holomorphic map defined by $C_1 (z) = \frac{1 + z}{1 - z}$. Thus we
define the following two semi-groups in $\mathbb{D}$,
$\phi_t, \tilde{\phi}_t : \mathbb{D} \mapsto \mathbb{D}$ defined by
$\phi_t = C_1^{-1} \circ \psi_t \circ C_1$ and
$\tilde{\phi}_t = C_1^{-1} ( -i \psi_t ( iC_1(z) ) )$. By construction
$\phi_t$ is a non elliptic group in $\mathbb{D}$ and $\tilde{\phi}_t$ is a non
elliptic semigroup in $\mathbb{D}$ that is not a group. Both semi groups are
conjugated to $\psi_t$ using the maps $z \mapsto C_1 (z)$ and
$z \mapsto i C_1 (z)$ respectively. Therefore $(\phi_t)$ being semi
conjugated to $(\psi_t)$ is not enough to capture the dynamical
behaviour of the semigroup.

**Definition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $\Omega$ be a Riemann
Surface, $h : \mathbb{D} \mapsto \Omega$ holomorphic and $(\psi_t)$ a continuous
group in $\Omega$ such that $(\phi_t)$ is semi conjugated to $(\psi_t)$
through $h$, namely the following diagram is commutative,

![Semiconjugation](/assets/report/tikzcd-2.JPG)

along with the condition

$$\bigcup_{t \leq 0} \psi_t \circ h(\mathbb{D}) = \Omega$$

Then the triple $(\Omega, h, \psi_t)$ is a semi-model for $(\phi_t)$.

If $h$ is injective, then $(\Omega, h, \psi_t)$ is a *model* for
$(\phi_t)$. Firstly we prove some simple properties of (semi)models,

**Proposition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$ and $(\Omega, h, \psi_t)$ a semi
model for $(\phi_t)$. Then

1.  $\psi_t \circ h(\mathbb{D}) \subset h(\mathbb{D})$ for all $t \geq 0$. In
    particular, if $(\Omega, h, \psi_t)$ is a model, then
    $\phi_t = h^{-1} \circ \psi_t \circ h$ on $h(\mathbb{D})$.

2.  If $(\phi_t)$ is elliptic, $(\psi_t)$ has a common fixed point.

**Proof**
1\) Using the commutative diagram 1,
$$\psi_t \circ h(\mathbb{D}) = h \circ \phi_t (\mathbb{D}) \subset h(\mathbb{D})$$

If $(\Omega, h, \psi_t)$ is a model, $h$ is injective and thus bijective
on its image, $h(\mathbb{D})$. Thus from the commutative diagram (13.1) it
follows that $\phi_t = h^{-1} \circ \psi_t \circ h$ on $h(\mathbb{D})$.

2\) If $(\phi_t)$ is elliptic the there exists $z_0 \in \mathbb{D}$ such that
$\phi_t (z_0) = z_0$, thus
$$\psi_t \circ h(z_0) = h \circ \phi_t (z_0) = h(z_0)$$

Thus $h(z_0)$ is a fixed point of $(\psi_t)$

Let $\phi_t (z) = C_1^{-1} ( e^t C_1(z) )$. $( \phi_t )$ is a hyperbolic
group in $\mathbb{D}$ and it has a model $(H, C_1, z \mapsto e^t z)$. We can
construct another model for $(\phi_t)$ using
$h : \mathbb{D} \mapsto S_\pi = \{ z \in \mathbb{C} \ | \ 0 < \Re(z) < \pi \}$ defined
by

$$h(z) = i \ln C_1(z) + \frac{\pi}{2}$$

where $\ln$ is the principal branch of the logarithm. Then
$(S_\pi, h, z \mapsto z + it)$ is a model for $(\phi_t)$. Therefore a
semigroup may have many different (semi) models, so to establish a
unique model for each semigroup, we need a way of mapping between (semi)
models.

**Definition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ and
$(\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$ be two semi models for
$(\phi_t)$. A morphism of holomorphic semi models
$\hat{\eta} : (\Omega, h, \psi_t) \mapsto (\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$
is a holomorphic map $\eta : \Omega \mapsto \tilde{\Omega}$ such that
the following are commutative diagrams.

![Semiconjugation](/assets/report/tikzcd-3.JPG)

**Example**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ be a
semi model for $(\phi_t)$. Let $id_\Omega : \Omega \mapsto \Omega$ be
the identity map, then

$$id_\Omega \circ h = h \qquad id_\Omega \circ \psi_t = \psi_t = \psi_t \circ id_\Omega$$

Therefore
$\hat{id}_\Omega : (\Omega, h, \psi_t) \mapsto (\Omega, h, \psi_t)$ is a
morphism of semi models.

**Example**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega^1, h^1, \psi_t^1)$,
$(\Omega^2, h^2, \psi_t^2)$, $(\Omega^3, h^3, \psi_t^3)$ be semi models
for $(\phi_t)$. Suppose
$\hat{\eta}_1 :  (\Omega^1, h^1, \psi_t^1) \mapsto (\Omega^2, h^2, \psi_t^2)$
and
$\hat{\eta}_2 :  (\Omega^2, h^2, \psi_t^2) \mapsto (\Omega^3, h^3, \psi_t^3)$
are morphisms of semi models, then we have a natural composition of semi
model morphisms,
$\hat{\eta} : (\Omega^1, h^1, \psi_t^1) \mapsto (\Omega^3, h^3, \psi_t^3)$
defined by,
$$\hat{\eta} = \hat{\eta}_2 \circ \hat{\eta}_1 = \widehat{\eta_2 \circ \eta_1}$$

The definition of a semi model morphism gives us a lot of structure,
which leads to the following two propositions,

**Proposition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ and
$(\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$ be two semi models for
$(\phi_t)$. If
$\hat{\eta} : (\Omega, h, \psi_t) \mapsto (\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$
is a morphism of semi models, then
$\eta : \Omega \mapsto \tilde{\Omega}$ is surjective.

**Proof**
Using the commutative diagrams for semi models and morphisms,

$$\begin{aligned}
\tilde{\Omega} &= \bigcup_{t \leq 0} \tilde{\psi}_t \circ \tilde{h} (\mathbb{D}) \\
&= \bigcup_{t \leq 0} \tilde{\psi}_t \circ \eta \circ h (\mathbb{D}) \\
&= \bigcup_{t \leq 0} \eta \circ \psi_t \circ h (\mathbb{D}) \\
&= \eta (\Omega)
\end{aligned}$$

The last equality follows from the continuity of $\eta$, as $\eta$ is holomorphic.

A surprising result of the definition for semi models morphisms is the
uniqueness of the morphisms,

**Proposition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ and
$(\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$ be two semi models for
$(\phi_t)$. Suppose
$\hat{\eta}, \hat{\mu} : (\Omega, h, \psi_t) \mapsto (\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$
are two morphisms of semi models, then $\hat{\eta} = \hat{\mu}$.

**Proof**
Equivalently, it suffices to show $\eta(z) = \mu(z)$ for all
$z \in \Omega$. The idea is to use the first commutative diagram of the
morphism to swap $\eta$ and $\mu$, more explicitly
$\eta \circ h = \tilde{h} = \mu \circ h$.

Let $z \in \Omega$, by the union condition, there exists $t \leq 0$ and
$w \in \mathbb{D}$ such that $z = \psi_t \circ h(w)$,

$$\begin{aligned}
\eta (z) &= \eta \circ \psi_t \circ h(w) \\
&= \tilde{\psi}_t \circ \eta \circ h(w) \\
&= \tilde{\psi}_t \circ \tilde{h} (w) \\
&= \tilde{\psi}_t \circ \mu \circ h(w) \\
&= \mu \circ \psi_t \circ h(w) \\
&= \mu(z)
\end{aligned}$$

Similarly to groups we can define a more restricted morphism,

**Definition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ and
$(\tilde{\Omega}, \tilde{h}, \tilde{\psi}\_t)$ be two semi models for
$(\phi_t)$. If $\hat{\eta} : (\Omega, h, \psi_t) \mapsto \tilde{\Omega}, \tilde{h}, \tilde{\psi}\_t)$
is a morphism of semi models and there exists a morphism of semigroups
$\hat{mu} : (\tilde{\Omega}, \tilde{h}, \tilde{\psi}\_t) \mapsto (\Omega, h, \psi_t)$
such that $\hat{\mu} \circ \hat{\eta} = id_\Omega$ and
$\hat{\eta} \circ \hat{\mu} = id_{\tilde{\Omega}}$ then $\hat{\eta}$ is
an isomorphism of semi models.

The previous proposition allows us to give some equivalent definitions
of semi model isomorphism.

**Theorem**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ and
$(\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$ be two semi models for
$(\phi_t)$. Let
$\hat{\eta} : (\Omega, h, \psi_t) \mapsto \tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$
be a morphism of semi models. Then the following are equivalent,

1.  $\eta$ is a biholomorphism.

2.  $\hat{\eta}$ is an isomorphism of semi models

3.  There exists a morphism of semi models
    $\mu : (\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t) \mapsto (\Omega, h, \psi_t)$

**Proof**
Since $\eta$ has a holomorphic inverse, this is the morphism in the
other direction and thus $(1) \to (2)$. By definition $(2) \to (3)$.
Suppose $(3)$ holds, then $\hat{\mu} \circ \hat{\eta}$ is an
endomorphism of $(\Omega, h, \psi_t)$ and thus
$\mu \circ \eta = id_\Omega$. Therefore $\eta$ is biholomorphic with
holomorphic inverse $\mu$, $(3) \to (1)$.

The final proposition before we prove the main result gives us a
morphism from a model to any semi model,

**Proposition**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Let $(\Omega, h, \psi_t)$ be a
model for $(\phi_t)$. Suppose
$(\tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$ is a semi model for
$(\phi_t)$, then there exists a unique morphism of semi models
$\hat{\eta} : (\Omega, h, \psi_t) \mapsto \tilde{\Omega}, \tilde{h}, \tilde{\psi}_t)$.

**Proof**
Uniqueness follows from Proposition 16.0.3. Let
$\Omega_t = \psi_{-t} \circ h(\mathbb{D})$ and
$\eta_t : \Omega_t \mapsto \tilde{\Omega}$ be defined by
$\eta_t = \tilde{\psi}\_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t$.

Let $0 \leq t \leq s$ and $z \in \Omega_t \cap \Omega_s$, then there
exists $w \in \mathbb{D}$ such that
$z = \phi_{-t} \circ h(w) = \phi_{-s} \circ h (w)$

$$\begin{aligned}
\psi_s \circ h (w) &= \psi_t \circ h (w) \\
h \circ \phi_s (w) &= h \circ \phi_t (w) \\
\text{Since $ h $ is injective,} \\
\phi_s (w) &= \phi_t (w) \\
\tilde{h} \circ \phi_s (w) &= \tilde{h} \circ \phi_t (w) \\
\tilde{\psi}_s \circ \tilde{h} (w) &= \tilde{\psi}_t \circ \tilde{h} (w)
\end{aligned}$$

Thus
$\tilde{\psi}\_{-s} \circ \tilde{h} (w) = \tilde{\psi}_{-t} \circ \tilde{h} (w)$
which be useful next. Now we show that $\eta_t (z) = \eta_s (z)$,

$$\begin{aligned}
\eta_t (z) &= \tilde{\psi}_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t (z) \\
&= \tilde{\psi}_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t \circ \phi_{-t} \circ h(w) \\
&= \tilde{\psi}_{-t} \circ \tilde{h} (w) \\
&= \tilde{\psi}_{-s} \circ \tilde{h} (w) \\
&= \tilde{\psi}_{-s} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_s \circ \phi_{-s} \circ h(w) \\
&= \tilde{\psi}_{-s} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_s (z) \\
&= \eta_s (z)
\end{aligned}$$

By definition, $\cup_{t \leq 0} \Omega_t = \Omega$. Let
$\eta : \Omega \mapsto \tilde{\Omega}$ be defined by
$\eta (z) = \eta_t (z)$ for some $t \geq 0$ such that $z \in \Omega_t$.
Therefore it suffices to show the two morphism diagrams commute.

Let $z \in \Omega$. Let $t \geq 0$ and $w \in \mathbb{D}$ such that
$z = \psi_{-t} \circ h(w)$.

$$\begin{aligned}
\eta \circ h(w) &= \tilde{\psi}_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t \circ h(w) \\
&= \tilde{\psi}_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ h \circ \phi_t (w) \\
&= \tilde{\psi}_{-t} \circ \tilde{h} \circ \phi_t (w) \\
&= \tilde{\psi}_{-t} \circ \tilde{\psi}_t \circ \tilde{h} (w) \\
&= \tilde{h} (w)
\end{aligned}$$

Similarly for the second diagram,

$$\begin{aligned}
\tilde{\psi}_t \circ \eta (z) &= \tilde{\psi}_t \circ \tilde{\psi}_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t (z) \\
&= \tilde{\psi}_{-t} \circ \tilde{\psi}_t \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t (z) \\
&= \tilde{\psi}_{-t} \circ \tilde{h} \circ \phi_t \circ h^{-1} |_{h(\mathbb{D})} \circ \psi_t (z) \\
&= \tilde{\psi}_{-t} \circ \tilde{h} \circ h^{-1} |_{h(\mathbb{D})} \psi_t \circ \psi_t (z) \\
&= \eta \circ \psi (z)
\end{aligned}$$

**Corollary**
Models of a semigroups $(\phi_t)$ are unique up to semi model isomorphism

The previous proposition gives a morphism in both directions, so by the
characterisation of semi model isomorphism, the models are isomorphic.

Thus if we consider a partial ordering on the semi models of a semigroup
defined by $A \geq B$ iff there exists a morphism of semimodels
$\hat{\eta} : A \mapsto B$, then a model, if it exists, is the unique
maximal element of the semi models of the semigroup.

We are now ready to prove the main result of this section

**Theorem**
Let $(\phi_t)$ be a semigroup in $\mathbb{D}$. Then there exists a unique (up to
semimodel isomorphism) model $(\Omega, h, \psi_t)$ for $(\phi_t)$.

**Proof**
Uniqueness follows from the previous corollary, so we proceed with
existence. The outline of the proof is as follows,

1.  Construct a topological space $\Omega$ and show it is a Riemann
    Surface

2.  Construct an intertwining map $h : \mathbb{D} \mapsto \Omega$ and show it is
    injective

3.  Construct an algebraic group $(\psi_n)$ in $\Omega$

4.  Show that $(\Omega, h, \psi_t)$ forms a model for $(\phi_n)$.

1\) Firstly we construct the topological space $\Omega$. Let
$[0, \infty)$ have the discrete topology. Define a relation on
$\mathbb{D} \times [0, \infty)$ as $(z, t) \sim (w, s)$ iff there exists
$u \in [0, \infty)$ such that $u \geq \max \{t, s\}$ and
$\phi_{u - t} (z) = \phi_{u - s} (w)$. $\sim$ is an equivalence
relation, each of the properties follow from $=$ being an equivalence
relation. Let $\Omega$ be the quotient space
$\mathbb{D} \times [0, \infty) / \sim$ and $\pi$ be the identification map.

To show $\Omega$ is a Riemann Surface, we need a holomorphic atlas
$\{ (h_t, \Omega_t)\}$ and we need to show that $\Omega$ is second
countable and path connected. Fix $t \geq 0$ and define
$h_t : \mathbb{D} \mapsto \Omega$ by $h_t (z) = \pi((z, t))$. $h_t$ is injective
as $\phi_t$ is injective. $h_t$ is continuous by the continuity of
$\pi$. To show $h_t$ is an open map let $U \subset \mathbb{D}$ be open. A set in
the quotient space is open if its preimage is open, so we need to check
if $\pi^{-1} ( \pi((U, t)))$ is open in $\mathbb{D} \times [0, \infty)$. As this
is a product space it suffices to check that the projections are open.
The projection onto $[0, \infty)$ is clearly open as $[0, \infty)$ has
the discrete topology. For the projection onto $\mathbb{D}$, note
$\{ z \in \mathbb{D} \ | \ (z, t) \in (U, t) \} = U$ as $\phi_n$ is injective.
Thus the projection $\pi^{-1} ( \pi((U, t)))$ onto $\mathbb{D}$ is the union of
open sets, which is open. Therefore $h_t |_{h(\mathbb{D})}$ is a homeomorphism.

Define $\Omega_t = h_t(\mathbb{D})$. Fix $s \geq 0$. Clearly
$(\phi_{t - s}, t) \sim (z, s)$ for all $t \geq s$. Thus,

$$h_s = h_t \circ \phi_{t - s}$$

In particular,

$$\Omega_s = h_s(\mathbb{D}) = h_t \circ \phi_{t - s} (\mathbb{D}) \subset h_t(\mathbb{D}) = \Omega_t$$

Therefore $\Omega = \cup_{t \in \mathbb{N}} \Omega_t$, and is therefore
second countable and path connected. It follows that
$\{ (h_t, \Omega_t) \}$ is a holomorphic atlas for $\Omega$ and $\Omega$
is a Riemann Surface.

2\) Let $h = h_0 : \mathbb{D} \mapsto \Omega$. $h$ is injective by construction.

3\) Define $\psi_s : \Omega \mapsto \Omega$ by

$$\phi_s (z) = h_{t - s} \circ h_t^{-1} \qquad z \in \Omega_t$$

Fix $s \geq 0$ then for all $t \geq s$,

$$\begin{aligned}
h_{t - s} \circ h^{-1} |_{\Omega_s} &= h_{t-s} \circ h_t^{-1} \circ h_s \circ h_s^{-1} \\
&= h_{t - s} \circ \phi_{t - s} \circ h_s^{-1} \\
&= h \circ h_s^{-1}
\end{aligned}$$

Thus the map $\psi_s$ is well defined. Since $h$ is injective, $\psi$ is
injective.

Let $w \in \Omega$ and fix $s \geq 0$. Let $t \geq s$ such that
$w \in \Omega_{t - s}$ then there exists $u \in \mathbb{D}$ such that
$w = h_{t - s} (u)$. Let $z = h_t (u)$.

$$\begin{aligned}
w &= h_{t - s} (u) \\
&= h_{t - s} \circ h_t^{-1} (z) \\
&= \psi_s (z)
\end{aligned}$$

Therefore $\psi_s$ is injective. Finally we need to show that $(\psi_n)$
forms an algebraic group. It suffices to show that
$\psi_t \circ \psi_s = \psi_{t + s}$. Let $t, s \geq 0$ and
$z \in \Omega$. There exists $u \geq t + s$ such that $s \in \Omega_u$.
Then $z = h_u (w)$ for some $w \in \mathbb{D}$.

$$\begin{aligned}
\psi_t \circ \psi_s (z) &= h_{u - t} \circ h_u^{-1} \circ h_{u - s} \circ h_u^{-1} (z) \\
&= h_{u - t} \circ h_u^{-1} \circ h_{u - s} \circ h_u^{-1} \circ h_u (w) \\
&= h_{u - t} \circ h_u^{-1} \circ h_{u - s} (w) \\
&= h_{u - t} \circ h_u^{-1} \circ h_u \circ \phi_{s} (w) \\
&= h_{u - t} \circ \phi_{s} (w) \\
&= h_u \circ \phi_t \circ \phi_s (w) \\
&= h_u \circ \phi_{t + s} (w) \\
&= h_{u - (t + s)} (w) \\
&= h_{u - (t + s)} \circ h_u^{-1} (z) \\
&= \psi_{t + s} (z)
\end{aligned}$$

The continuity of $(\psi_n)$ follows from the continuity of $(\phi_n)$ (see
[4]). Therefore $(\psi_n)$ is an algebraic group in $\Omega$.

4\) Let $t \geq 0$, since $h(\mathbb{D}) \subset \Omega_t$,

$$\psi_t \circ h = h \circ h_t^{-1} \circ h = h \circ \phi_t$$

Since $\psi_{-t} = h_t \circ h^{-1}$ on $h(\mathbb{D})$,

$$\bigcup_{t \geq 0} \psi_{-t} \circ h(\mathbb{D}) = \bigcup_{t \geq 0} h_t (\mathbb{D}) = \Omega$$

Therefore $(\Omega, h, \psi_n)$ is a model for $(\phi_n)$.

We can extend the Denjoy Wolff theorem to continuous semigroups
[4], and use this to classify semigroups similarly to
holomorphic self maps,

**Theorem**
Let $(\phi_t)$ be a non trivial semi groups in $\mathbb{D}$. Then, all iterates
different from the identity have the same Denjoy-Wolff point
$\tau \in \overline{\mathbb{D}}$.

**Theorem**
Let $(\phi_n)$ be a semigroup in $\mathbb{D}$. Then,

1.  $(\phi_n)$ is the trivial semigroup iff $(\phi_n)$ has a holomorphic
    model $(\mathbb{D}, id_\mathbb{D}, z \mapsto z)$

2.  $(\phi_n)$ is a group of elliptic automorphisms iff $(\phi_n)$ has a
    holomorphic model $(\mathbb{D}, h, z \mapsto e^{-i \theta} z)$,
    $\theta \in \mathbb{R} - \{ 0\}$

3.  $(\phi_n)$ is elliptic, not a group iff $(\phi_n)$ has a holomorphic
    model $(\mathbb{C}, h, z \mapsto e^{- \lambda t} z)$, $\lambda \in \mathbb{C}$ such
    that $\Re \lambda > 0$

4.  $(\phi_n)$ is hyperbolic iff $(\phi_n)$ has a holomorphic model
    $(\mathbb{S}_\frac{\pi}{\lambda}, h, z \mapsto z + it)$,
    $\lambda > 0$

5.  $(\phi_n)$ is parabolic of positive hyperbolic step iff $(\phi_n)$
    has a holomorphic model either of the form
    $(\mathbb{H}, h, z \mapsto z + it)$ or
    $(\mathbb{H}^-, h, z \mapsto z + it)$.

6.  $(\phi_n)$ is parabolic of zero hyperbolic step iff $(\phi_n)$ has a
    holomorphic model $(\mathbb{C}, h, z \mapsto z + it)$

# Conclusion

In this report we have studied the geometric properties of the Poincaré
disk and Upper half plane with the hyperbolic metric. We studied the
dynamics of iterating Möbius transformations and characterised the
different types. We introduced algebraic semigroups and models, one of
the tools for characterising semigroups. Further research into this area
could include studying other tools for characterisation such as
infinitesimal generators which has applications to differential
equations. Additionally the reference for this report ([4])
took an analytic approach to defining semigroups, a more abstract
approach using using tangent bundles of intervals would allow the use of
more powerful mathematical techniques as these spaces have been
thoroughly studied, see [3].

# References

## Articles

[1] W. Abikoff. “The Uniformization Theorem”. In: The American Mathematical Monthly 88(8)
(1981), pages 574–592.

[3] M. F. Atiyah. “Vector Bundles Over an Elliptic Curve”. In: Proceedings of the London
Mathematical Society s3-7.1 (1957), pages 414–452.

## Books

[2] Lars Ahlfors. Complex Analysis. McGraw-Hill, 1979, page 134.

[4] Filippo Bracci, Manuel D. Contreras, and Santiago Díaz-Madrigal. Continuous Semigroups
of Holomorphic Self-maps of the Unit Disk. Springer, 2020.
[5] Manfredo do Carmo. Differential Geometry of Curves and Surfaces. 2nd edition. Dover,
2016, pages 267–278.

[6] Alfred Gray. Modern Differential Geometry of Curves and Surfaces with Mathematica.
3rd edition. Chapman and Hall/CRC, 2006, pages 504–507.

[7] Linda Keen and Nikola Lakic. Hyperbolic Geometry from a Local Viewpoint. London
Mathematical Society, 2007, pages 46–50.

[8] Roger Penrose. The Road To Reality: A Complete Guide to the Laws of the Universe. Jonathan
Cape, 2004, page 45.

[9] H. L. Royden and P. M. Fitzpatrick. Real Analysis. 4th. Pearson Education Inc, 2010, page 94.

[10] Walter Rudin. Real and Complex Analysis. 3rd. McGraw–Hill Book Co, 1987, page 293.
