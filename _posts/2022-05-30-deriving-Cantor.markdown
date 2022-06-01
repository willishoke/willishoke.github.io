---
layout: post
title:  "Deriving the Cantor pairing function: a hidden geometric series"
date:   2022-05-30
# categories: python, math

---

![Cantor pairing function](/assets/images/cantor.svg)

The Cantor pairing function is a bijective mapping from the set of all pairs of natural numbers to the set of all natural numbers. We can visualize it in several different ways: numerically, as a path, or as a manifold in 3-dimensional space.

![Cantor pairing function (with finite diffences)](/assets/images/diff.svg)

The standard way to derive the Cantor pairing function is rather technical, and involves recurrance relations. But there is another method involving a simple trick, one which can be helpful when studying other sequences. Given a sequence of $n$ elements, any element $x_k \in (x_1 \dots x_n)$ is equal to the following sum of differences, which forms a telescoping series:

$x_k = (x_k - x_{k-1}) + (x_{k-1} - x_{k-2}) + \dots + (x_2 - x_1) + x_1$

Let $f(x, y)$ represent our candidate pairing function. First let's hold $y = 0$ constant to solve for $f(x, 0)$:

$f(x, 0) = f(0,0) + \big(f(1,0)-f(0,0)\big) + \big(f(2,0) - f(1,0)\big) + \dots + \big(f(x, 0) - f(x-1, 0)\big)$

Looking at the figure above, we can see that this forms a geometric series:

$f(x, 0) = 1 + 2 + \dots + x$

$= \displaystyle\sum_{i=1}^{x} i$

Next let's hold $x$ constant. According to the same logic as above, we can observe

$f(x, y) = f(x, 0) + \big(f(x, 1) - f(x, 0)\big) + \dots + \big(f(x, y) - f(x, y-1)\big)$

This can be reduced to:

$f(x, y) = \bigg(\displaystyle\sum_{i=1}^{x} i\bigg) + \bigg(\sum_{i=x+2}^{x+y+1} i\bigg)$

$= \bigg(\displaystyle\sum_{i=1}^{x+y+1}i\bigg)-(x+1)$

$= \displaystyle\frac{(x+y+1)(x+y+2)}{2}-(x+1)$

$= \displaystyle\frac{(x+y)(x+y+1)}{2}+y$

Now, we can verify our identity using the `sympy` package:

```
>>> from sympy.abc import i, x, y
>>> from sympy import Sum, expand
>>> f1 = Sum(i, (i, 1, x + y + 1)).doit() - (x + 1)
>>> f2 = expand((((x + y) * (x + y + 1) / 2) + y))
>>> f1 == f2
True
```
The source code used to generate all figures in this post can be found here.