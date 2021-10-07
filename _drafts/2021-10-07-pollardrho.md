---
title: Pollard $\rho$ Algorithm
date: 2021-10-07
categories: [Algorithms]
tags: [primes]     # TAG names should always be lowercase
math: true
comments: false
---
The Pollard $\rho$ algorithm allows us...

The Pollard $\rho$ implementation in Python is as follows,
```python
def pollard_rho(n: int) -> int:
    for i in range(n//2):
        x = random.randint(2,n-1)
    var = pollard_rho_algo(n, x)
    if var is not None:
        return var
    return 'No factor found'

def pollard_rho_algo(n: int, x: int) -> int:
    y = x
    k = 2
    for i in range(100):
        x = (x**2 - 1) % n
        d = gcd(y - x, n)
        if d != 1 and d != n:
            return d
        if i == k:
            y = x
            k = 2*k
```
