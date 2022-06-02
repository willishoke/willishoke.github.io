---
layout: post
title:  "Finding a closed form for the boustrodephon pairing function"
date:   2022-05-30 
categories: python math
usemath: true
---

![Boustrodephon pairing function](/assets/images/boustrodephon.svg)

Like the standard Cantor pairing function, the boustrodephon (Greek: "Ox plowing a field") variant is monotonic and has a continuous embedding in the reals. It can be obtained by applying a nonlinear transformation to the original mapping, with the slope along each diagonal alternating between positive and negative values.

![Boustrodephon pairing function](/assets/images/boustrodephon_manifold.svg)

First, we observe that the Cantor pairing function has a simple variant with the $x$ and $y$ axes swapped. Second, note that the sum of the values of any two coordinates alternates in parity along the diagonal, so we can use a linear combination of the original Cantor function and its mirror variant, with the proportion of each determined by a trigonometric indicator function. In this way, we can get a smooth and continuous real-valued extension of the Boustrodephon variant.

$\frac{1}{2}\bigg(cos\big(\pi(x+y+1)\big)f(y,x) + cos\big(\pi(x+y)\big)f(x,y)\bigg)$

In Python:

```python
def boustrodephonPair(x, y):
    even_term = 1/2 * (1 + np.cos(np.pi*(x+y))) * cantorPair(y, x)
    odd_term = 1/2 * (1 + np.cos(np.pi*(x+y+1))) * cantorPair(x, y)
    return even_term + odd_term
```


The source code used to generate all figures in this post can be found here.