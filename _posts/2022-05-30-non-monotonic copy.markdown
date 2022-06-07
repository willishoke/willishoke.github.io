---
layout: post
title:  "Non-monotonic pairing functions"
date:   2022-05-30 
usemath: true
---

There are in fact uncountably many non-monotonic pairing functions. One interesting family is obtained by applying some permutation $p : \mathbb{N} \rightarrow \mathbb{N}$ to the $x$ and $y$ inputs to the Cantor pairing function. We could, for example, swap even and odd inputs:

\$\$eggCarton(x, y) = cantorPair\big(x + cos(\pi x), y + cos(\pi y)\big)\$\$

When plotted, the manifold has a signature "egg carton" shape:
![Egg carton pairing function](/assets/images/eggcartonmanifold.svg)

The path traced by connecting each successive output value resembles a weave structure:

![Egg carton pairing function](/assets/images/eggcarton.svg)

More complex permutations of the input result in more intricate patterns. Here we swap pairs of adjacent rows and columns:

![Double egg carton pairing function](/assets/images/doubleeggcarton.svg)

These examples have no practical utility, but they certainly yield beautiful visualizations.

The source code used to generate all figures in this post can be found [here](https://github.com/willishoke/notebooks/blob/main/pairing_functions.ipynb).

