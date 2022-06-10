---
layout: post
title:  "Turing Patterns in higher dimensions"
date:   2022-06-01
usemath: true
---

In my last post I explored a method for generating Turing patterns in two dimensions. This method can easily be extended to 3 or more dimensions:

\$\$ f(x, y, z) = \sum{U_{r,s,t}} \exp \bigg(-\frac{1}{2}\big((x - hr)^2 + (y - hs)^2 + (z - ht)^2\big)\bigg)\$\$

![3D Turing Countour Map](/assets/images/turing3D1.svg)

Unhappy with the lengthy running time required to generate a single example, I tried using the `numba` package to enable just-in-time compilation of Python loops to optimize my implementation. Unfortunately, it turned out that Python wasn't the bottleneck here - it was simply the large number of matrix multiplications. 

I wanted to generate larger three dimensional patterns, so I came up with a compromise: reduce the number of sampling points, use a contour-finding algorithm to find adjacent points along the boundaries of shapes, and use splines to smoothly interpolate between the sample points. Using this solution, I was able to compute larger 3 dimensional patterns in under an hour. 

![Large 3D Turing Contour Map](/assets/images/turing3D2.svg)

