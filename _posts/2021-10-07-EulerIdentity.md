---
title: Euler Identity
date: 2021-10-07
categories: [Complex Analysis]
tags: [Euler]     # TAG names should always be lowercase
math: true
comments: false
---
Let $n \in \mathbb{N}$. Prove that
\begin{equation}
I_n := \int_0^{2\pi} \cos^{2n} (\theta) d\theta = 2 \pi \frac{1 \cdot 3 \cdot 5 \cdot \cdot \cdot (2n -1)}{2 \cdot 4 \cdot 6 \cdot \cdot \cdot (2n)}
\end{equation}
Let
\begin{equation}
J_n := \int_{\{|z| = 1\}} \bigg( z + \frac{1}{z} \bigg)^{2n} \frac{dz}{z}
\end{equation}
Using Euler's Identity $e^{i \theta} = \cos(\theta) + i\sin(\theta)$ we can rewrite $\cos(\theta)$,
\begin{equation}
\cos(\theta) = \frac{e^{i\theta} + e^{-i\theta}}{2}
\end{equation}
\begin{equation}
I_n = \int_0^{2\pi} \bigg(\frac{e^{i\theta} + e^{-i\theta}}{2} \bigg)^{2n} d\theta
\end{equation}
making the substitution $z = e^{i \theta}$ to the integral $I_n$, the interval 0 to $2\pi$ becomes the unit circle,
\begin{equation}
dz = i e^{i\theta} d\theta
\end{equation}
\begin{equation}
\Rightarrow \int_{\{|z| = 1\}} \bigg( \frac{z + z^{-1}}{2} \bigg)^{2n} \frac{dz}{iz}
\end{equation}
\begin{equation}
= \frac{-i}{2^{2n}} \int_{\{|z| = 1\}} \bigg( z + \frac{1}{z} \bigg)^{2n} \frac{dz}{z}
\end{equation}
\begin{equation}
I_n =  \frac{-i}{2^{2n}} J_n
\end{equation}
Now we write $J_n$ in the form
\begin{equation}
\int_{\{|z| = 1\}} \frac{f(z)}{(z-z_0)^{2n+1}} dz
\end{equation}
\begin{equation}
J_n = \int_{\{|z| = 1\}} \bigg( z + \frac{1}{z} \bigg)^{2n} \frac{dz}{z}
\end{equation}
\begin{equation}
= \int_{\{|z| = 1\}} \frac{(z^2 + 1)^{2n}}{z^{2n}} \frac{dz}{z}
\end{equation}
\begin{equation}
= \int_{\{|z| = 1\}} \frac{(z^2 + 1)^{2n}}{z^{2n+1}} dz
\end{equation}
Therefore $z_0 = 0$ and $f(z) = (z^2+1)^{2n}$ \newline \newline
Using the Cauchy Integral Formula, we show that
\begin{equation}
\int_{\{|z| = 1\}} \frac{f(z)}{(z-z_0)^{2n+1}} dz = \frac{2i \pi}{(2n)!} f^{(2n)}(z_0)
\end{equation}
The Cauchy Integral Formula is given by,
\begin{equation}
f(z_0) = \frac{1}{2i\pi} \int_C \frac{f(z)}{z-z_0} dz
\end{equation}
where $f(z)$ is an analytic function, $C$ is a positively oriented simple closed curve and $z_0$ any point inside the domain bounded by $C$. Differentiating n times with respect to $z_0$
\begin{equation}
f^{(n)}(z_0) = \frac{n!}{2i\pi} \int_C \frac{f(z)}{(z-z_0)^{n+1}} dz
\end{equation}
where $f(z)$ is an analytic function, $C$ is a positively oriented simple closed curve and $z_0$ any point inside the domain bounded by $C$. Rearranging for the integral on the RHS, redefining $n:=2n$ and letting $C$ be the curve $|z| = 1$,
\begin{equation}
f^{(2n)}(z_0) \frac{2i\pi}{(2n)!} = \int_{\{|z| = 1\}} \frac{f(z)}{(z-z_0)^{2n+1}} dz
\end{equation}
Putting together the above pieces we obtain the value of $I_n$. \newline \newline
Let $f(z) = (z^2+1)^{2n}$, $z_0 = 0$, and substitute into Equation (4.3), the LHS simply becomes the integral $J_n$,
\begin{equation}
J_n = \frac{2i\pi}{(2n)!} f^{(2n)}(0)
\end{equation}
Using the binomial expansion formula, we can expand $f(z)$
\begin{equation}
f(z) = \sum_{m=0}^{2n} \frac{(2n)!}{m!(2n-m)!} z^{2m}
\end{equation}
To substitute into Equation (4.3), we need to differentiate $f(z)$ $2n$ times, and then set $z = 0$. As a result all terms vanish except when $m = n$. The $m = n$ term is given by,
\begin{equation}
\frac{(2n)!}{(n!)^2} z^{2n}
\end{equation}
Differentiating the expresion above $2n$ times and substituting into $f^{(2n)}(0)$ gives,
\begin{equation}
f^{(2n)}(0) = \bigg( \frac{(2n)!}{n!} \bigg)^2
\end{equation}
Therefore,
\begin{equation}
J_n = \frac{2\pi i (2n)!}{(n!)^2}
\end{equation}
Substituting $J_n$ into Equation (4.1),
\begin{align}
I_n &=  \frac{-i}{2^{2n}} J_n \\
&= 2 \pi \frac{(2n)!}{2^{2n}(n!)^2} \\
&= 2 \pi \frac{(2n)!}{2^nn!} \frac{1}{2^nn!}
\end{align}
The first fraction can be rewritten as $(2n-1)!!$ where !! represents the double factorial, the product of all odd numbers up to $2n-1$. The $2^n$ term halves all of the even numbers in the $(2n)!$ term to give $n!$ which is then cancelled out by the $n!$ in the denominator and we are left with all of the odd numbers up to $2n$ or more precisely $2n-1$. \newline
The second fraction becomes $(2n)!!$, the product of all even numbers up to $2n$ as we multiple each term in $n!$ by 2.
\begin{equation}
\Rightarrow I_n = 2 \pi \frac{(2n-1)!!}{(2n)!!}
\end{equation}
\begin{equation}
= 2 \pi \frac{1 \cdot 3 \cdot 5 \cdot \cdot \cdot (2n -1)}{2 \cdot 4 \cdot 6 \cdot \cdot \cdot (2n)} \text{ } \QED
\end{equation}
