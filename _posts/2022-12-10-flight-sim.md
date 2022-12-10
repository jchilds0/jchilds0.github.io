---
title: Flight Simulator
date: 2022-12-10 12:00
categories: [Game Development]
tags: [game dev, curves, geometry]     # TAG names should always be lowercase
math: true
comments: false
---

The aim of this project is to develop a flight simulator controlled using torsion and curvature.
It is built in python using the panda3D graphics library.

<img src="/assets/flight-sim/image.PNG">

## Download

The game can be downloaded from [jchilds0/flight-sim/releases](https://github.com/jchilds0/flight-sim/releases). Download the latest
arhive corresponding to your system, extract the archive and run 'flight-sim.exe'.

The source code can be viewed at [jchilds0/flight-sim](https://github.com/jchilds0/flight-sim/)

## Preliminaries

A curve $ \gamma $ is a map from $ \mathbb{R} $ to $ \mathbb{R}^3 $. We assume the curve
is unit speed to simplify the formulas, $ |\gamma'(s)| = 1 $. Then define the tangent
vector $ T $ by $ T(s) = \gamma'(s) $. Similarily define the normal vector $ N $, as the unit
vector in the direction of $ T'(s) $. Finally define $ B(s) $ as the unit vector in
the direction of $ T(s) \times N(s) $, where $ \times $ is the cross product in
$ \mathbb{R}^3 $. Finally the curvature $ \kappa $ at a point $ \gamma(s) $ is defined
as the length of T'(s), $ \kappa(s) = |T'(s)| $. And the torsion $ \tau $ at a point
$ \gamma(s) $ is defined $ - N(s) \cdot B'(s) $, where $ \cdot $ is the dot product.

The triple $(T(s), N(s), B(s))$ is called the Frenet-Serre Frame and forms an orthogonal
basis for $ \mathbb{R}^3 $. The quantities also satisfy a system of differential equation
called the [Frenet-Serre Formulas](https://en.wikipedia.org/wiki/Frenet%E2%80%93Serret_formulas)

$$ T'(s) = \kappa N(s) $$

$$ N'(s) = - \kappa T(s) + \tau B(s) $$

$$ B'(s) = - \tau N(s) $$

## Mechanics

We start with an initial position $ \gamma(0) $, $T(0) = (0, 1, 0)$, $N(0) = (1, 0, 0)$,
$B(0) = (0, 0, 1)$. Then we add the formula $ \gamma'(s) = T(s) $ to the Frenet-Serre
Formulas, and solving this system numerically we obtain the next position. We also solve
further ahead to draw a curve on the screen for the user, showing them the current curve they are on.

## Interpretation

Curvature can be thought of as how much a curve curves, a curve with constant curvature
is a circle of radius $ 1 / \kappa $. Torsion measures how much $ \gamma $ is twisting out
of the 'osculating plane'. A curve with torsion 0 is contained in a plane.


