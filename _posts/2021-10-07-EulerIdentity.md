---
title: Integral of Even Powers of Cosine
date: 2021-10-07 15:00
categories: [Complex Analysis]
tags: [euler, contour]     # TAG names should always be lowercase
math: true
comments: false
---
Let $n \in \mathbb{N}$.

$$I_n := \int_0^{2\pi} \cos^{2n} (\theta) d\theta = 2 \pi \frac{1 \cdot 3 \cdot 5 \cdot \cdot \cdot (2n -1)}{2 \cdot 4 \cdot 6 \cdot \cdot \cdot (2n)}$$

We begin by relating $I_n$ to the following integral

$$J_n := \int_{\{|z| = 1\}} \bigg( z + \frac{1}{z} \bigg)^{2n} \frac{dz}{z}$$

Using Euler's Identity $e^{i \theta} = \cos(\theta) + i\sin(\theta)$, we can rewrite
$\cos(\theta)$,

$$\cos(\theta) = \frac{e^{i\theta} + e^{-i\theta}}{2}$$

$$I_n = \int_0^{2\pi} \bigg(\frac{e^{i\theta} + e^{-i\theta}}{2} \bigg)^{2n} d\theta$$

making the substitution $z = e^{i \theta}$ to the integral $I_n$, the interval 0 to $2\pi$ becomes the unit circle,

$$dz = i e^{i\theta} d\theta$$

$$\Rightarrow \int_{\{|z| = 1\}} \bigg( \frac{z + z^{-1}}{2} \bigg)^{2n} \frac{dz}{iz}$$

$$= \frac{-i}{2^{2n}} \int_{\{|z| = 1\}} \bigg( z + \frac{1}{z} \bigg)^{2n} \frac{dz}{z}$$

$$I_n =  \frac{-i}{2^{2n}} J_n$$

In order to evaluate this integral, we convert it to a form to apply the Cauchy's Theorem, namely

$$\int_{\{|z| = 1\}} \frac{f(z)}{(z-z_0)^{2n+1}} dz$$

For an appropriate $z_0 \in \mathbb{C}$ and an appropriate analytic function $f(z)$.

$$J_n = \int_{\{|z| = 1\}} \bigg( z + \frac{1}{z} \bigg)^{2n} \frac{dz}{z}$$

$$= \int_{\{|z| = 1\}} \frac{(z^2 + 1)^{2n}}{z^{2n}} \frac{dz}{z}$$

$$= \int_{\{|z| = 1\}} \frac{(z^2 + 1)^{2n}}{z^{2n+1}} dz$$

Therefore $z_0 = 0$ and $f(z) = (z^2+1)^{2n}$. The Cauchy Integral Formula is given by,

$$f(z_0) = \frac{1}{2i\pi} \int_C \frac{f(z)}{z-z_0} dz$$

where $f(z)$ is an analytic function, $C$ is a positively oriented simple closed curve and $z_0$ any point inside the
domain bounded by $C$.

Differentiating n times with respect to $z_0$

$$f^{(n)}(z_0) = \frac{n!}{2i\pi} \int_C \frac{f(z)}{(z-z_0)^{n+1}} dz$$

Rearranging for the integral on the RHS, redefining $n:=2n$ and letting $C$ be the curve $|z| = 1$,

$$f^{(2n)}(z_0) \frac{2i\pi}{(2n)!} = \int_{\{|z| = 1\}} \frac{f(z)}{(z-z_0)^{2n+1}} dz$$

Putting together the above pieces we obtain the value of $I_n$.

Let $f(z) = (z^2+1)^{2n}$ (which is entire as f is a polynomial), $z_0 = 0$, and substitute into the above formula, the RHS becomes the integral $J_n$,

$$J_n = \frac{2i\pi}{(2n)!} f^{(2n)}(0)$$

Using the binomial expansion formula, we can expand $f(z)$

$$f(z) = \sum_{m=0}^{2n} \frac{(2n)!}{m!(2n-m)!} z^{2m}$$

To substitute f into the following equation,

$$J_n = \frac{2i\pi}{(2n)!} f^{(2n)}(0)$$

we need to differentiate $f(z)$ $2n$ times, and then set $z = 0$. As a result all
terms vanish except when $m = n$. The $m = n$ term is given by,

$$\frac{(2n)!}{(n!)^2} z^{2n}$$

Differentiating the expresion above $2n$ times and substituting into $f^{(2n)}(0)$ gives,

$$f^{(2n)}(0) = \bigg( \frac{(2n)!}{n!} \bigg)^2$$

Therefore,

$$J_n = \frac{2\pi i (2n)!}{(n!)^2}$$

Substituting $J_n$ into the equation we found at the start relating $I_n$ to $J_n$,

$$I_n =  \frac{-i}{2^{2n}} J_n$$

$$= 2 \pi \frac{(2n)!}{2^{2n}(n!)^2}$$

$$= 2 \pi \frac{(2n)!}{2^nn!} \frac{1}{2^nn!}$$

The first fraction can be rewritten as $(2n-1)!!$ where !! represents the double factorial, the product of all odd
numbers up to $2n-1$. The $2^n$ term halves all of the even numbers in the $(2n)!$ term to give $n!$ which is then
cancelled out by the $n!$ in the denominator and we are left with all of the odd numbers up to $2n$ or more precisely
$2n-1$. The second fraction becomes $(2n)!!$, the product of all even numbers up to $2n$ as we multiple each term in
$n!$ by 2.

$$\Rightarrow I_n = 2 \pi \frac{(2n-1)!!}{(2n)!!} = 2 \pi \frac{1 \cdot 3 \cdot 5 \cdot \cdot \cdot (2n -1)}{2 \cdot 4 \cdot 6 \cdot \cdot \cdot (2n)} $$
